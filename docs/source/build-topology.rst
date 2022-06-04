Build Topology
=====

.. _overview:

Überblick
----------------

Das Build Topology System bietet die Möglichkeit GNS3 Projekte von Virtuelle Hosts zu sehen, hinzuzufügen und zu löschen. Außerdem kann man Projekte von einem virtuellen Host zu einem oder mehreren anderen kopieren. Das kopieren oder auch "clonen" wird angeboten um Lehrern einen bequemen Weg zu bieten begonnene, falsche oder auch fertige Topologien an Schüler zu senden, damit diese nicht von "null" starten müssen. So können Schüler an einer vorgegebenen Topologie weiterarbeiten, eine fertige weiterverwenden oder falsche "troubleshooten" und richtigstellen.

Überblick der Features
--------------------------------
Bei Start unseres Tools landet mal zu allererst auf der Dashboard Page. Hier werden abgesehen von allen virtuellen Hosts mit denen eine Verbindung besteht auch ein Button um einen virtuellen Hosts hinzuzufügen (eine Verbindung mit diesem aufbauen) angezeigt.

.. image:: images/dashboard-page.PNG
  :width: 600
  :alt: Dashboard Page

Virtual Host Ansicht
^^^^^^^^^^^^^^^^^^^^^^^^^^
Hier kann man nun auf eine der Boxen, welche einen virtuellen Host repräsentieren, klicken und kommt dann auf eine Page mit der man eine detailreichere Ansicht eines virtuellen Hosts sieht. Man sieht alle GNS3 Projekte, welche sich auf der virtuellen Maschine befinden, in einer vertikalen Reihe. Darunter befinden sich zwei Buttons, einmal einer der den User wieder zu der Dashboard Page bringt und einmal einen Button um ein GNS3 Projekt auf dem virtuellen Host hinzuzufügen.

.. image:: images/virtuel-host-detail.PNG
  :width: 600
  :alt: Virtual Host Page
  
Add Virtual Host Ansicht
^^^^^^^^^^^^^^^^^^^^^^^^^^
Zurück bei der Dashboard Page kann man alternativ auch auf den "Add VM" Button klicken und kommt somit zu dieser Ansicht bei der man die IP-Addresse der virtuellen Machine, den Port und ... angeben muss. Läuft alles nach Plan wird auf der Dashboard Page nun eine zusätzliche VM angezeigt.

.. image:: images/virtuel-host-add.PNG
  :width: 600
  :alt: Add Virtual Host Page
  
Aufbau
----------------

Hier sieht man den Aufbau der Build-Topology Funktionen:

.. image:: images/gns3-api-class-diagram.svg
  :width: 600
  :alt: GNS3-API Klassendiagramm
   
Verwendete Funktionen
----------------

namespaces/build-topology/views.py

.. code-block:: python

  @login_required()
  def virtualmachines(request):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      return render(request, "admin/Build Topology/Virtual Machines/virtual_machines.html")

.. code-block:: python

  @login_required()
  def projects(request, vm=None):
      if not request.user.is_superuser:
          return render(request, "user/404.html")

      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      virtual_machine = virtual_machines[vm]

      return render(request, "admin/Build Topology/Projects/projects.html", 
                    context={"projects": virtual_machine.get_projects(), "virtual_machine": vm})

.. code-block:: python

  @login_required()
  def reload(request):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      for vm in virtual_machines.values():
          vm.init_projects()
      return redirect("/")

.. code-block:: python

  @login_required()
  def devices(request, vm, project):
      if not request.user.is_superuser:
          return render(request, "user/404.html")

      if not vm:
          vm = request.GET.get('vm', '')

      if not project:
          project = request.GET.get('projects', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      projekte = virtual_machines[vm].get_projects()

      if project not in projekte:
          return render(request, "admin/404.html")

      projekt = projekte[project]

      return render(request, "admin/Build Topology/Devices/devices.html",
                    context={"devices": projekt.get_devices().items(), "project": project, "virtual_machine": vm})

.. code-block:: python

  @login_required()
  def config(request, vm, project):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      projekte = virtual_machines[vm].get_projects()
      if project not in projekte:
          return render(request, "admin/404.html")

      return render(request, "admin/Build Topology/Devices/conf_devices.html",
                    context={"devices": projekte[project].get_devices(), "project": project, "virtual_machine": vm})

.. code-block:: python

  @login_required()
  def push_config_to_devices(request, vm, project):
      if not request.user.is_superuser:
          return render(request, "user/404.html")

      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      projekte = virtual_machines[vm].get_projects()
      if project not in projekte:
          return render(request, "admin/404.html")

      projekt = projekte[project]
      devices = projekt.get_devices()

      geraete = [device for device in devices if request.POST.get(device, "")]
      timesleep = request.POST.get("timesleep", "")
      config = request.POST.get("config", "")
      
      for geraet in geraete:
        thread = threading.Thread(target=projekt.write_config, args=(geraet, config, timesleep))
        thread.start()

      return render(request, "admin/Build Topology/Devices/conf_devices.html",
                    context={"devices": projekt.get_devices(), "project": project, "virtual_machine": vm})


.. code-block:: python

  @login_required()
  def choose_vm_to_clone_from(request):
      if not request.user.is_superuser:
          return render(request, "user/404.html")

      return render(request, "admin/Build Topology/Clone Project/choose_vm_to_clone_from.html")

.. code-block:: python

  @login_required()
  def choose_project_to_clone(request, vm):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      return render(request, "admin/Build Topology/Clone Project/choose_project_to_clone.html",
                    context={"projects": virtual_machines[vm].get_projects(), "virtual_machine": vm})

.. code-block:: python

  @login_required()
  def select_what_vms_to_clone_to(request, vm):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      projekte = virtual_machines[vm].get_projects()

      project = request.POST.get("projekt", "")
      if project not in projekte:
          return render(request, "admin/404.html")

      return render(request, "admin/Build Topology/Clone Project/select_vms.html",
                    context={"project": project, "virtual_machine": vm})

.. code-block:: python

  @login_required()
  def clone_project(request, vm, project):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      projekte = virtual_machines[vm].get_projects()
      if project not in projekte:
          return render(request, "admin/404.html")

      vms = [virtual_machine for vm, virtual_machine in virtual_machines.items() if request.POST.get(vm, "")]
      vm = virtual_machines[vm]
      vm.clone_project(project, vms)

      return redirect("/build_topology/relaod")

.. code-block:: python

  @login_required()
  def add_vm(request):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if request.method == "GET":
          return render(request, "admin/Build Topology/Virtual Machines/add_vm.html")
      name = request.POST.get("name", "")
      ip = request.POST.get("ip", "")
      port = request.POST.get("port", "")
      with open('assets/gns3_api_calls/virtual_machines', 'a') as file:
          file.write(f"\n{name},{ip},{port}")
      try:
          get_virtual_machines("assets/gns3_api_calls/virtual_machines")
      except:
          return render(request, "admin/404.html")
      return redirect("/")

.. code-block:: python

  @login_required()
  def add_project(request, vm):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if request.method == "GET":
          return render(request, "admin/Build Topology/Projects/add_project.html", context={"vm": vm})
      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      name = request.POST.get("name", "")
      virtual_machines[vm].create_project(name)
      return redirect(f"/build_topology/projects/{vm}")

.. code-block:: python

  @login_required()
  def add_device(request, vm, project):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if request.method == "GET":
          return render(request, "admin/Build Topology/Devices/create_device.html",
                        context={"project": project, "virtual_machine": vm})

      name = request.POST.get("name", "")
      node_type = request.POST.get("node_type", "")

      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      projekte = virtual_machines[vm].get_projects()
      if project not in projekte:
          return render(request, "admin/404.html")

      projekt = projekte[project]

      projekt.create_device(name, node_type)
      return render(request, "admin/Build Topology/Devices/devices.html",
                    context={"devices": projekt.get_devices().items(), "project": project, "virtual_machine": vm})

.. code-block:: python

  def edit(request, vm, project, device):
      if not request.user.is_superuser:
          return render(request, "user/404.html")
      if request.method == "GET":
          return render(request, "admin/Build Topology/Devices/edit.html",
                        context={"device": device, "project": project, "virtual_machine": vm})

      if not vm:
          vm = request.GET.get('vm', '')

      if vm not in virtual_machines:
          return render(request, "admin/404.html")

      projekte = virtual_machines[vm].get_projects()
      if project not in projekte:
          return render(request, "admin/404.html")

      projekt = projekte[project]
      if 'start' in request.POST:
          projekt.start_device(device)
      elif 'stop' in request.POST:
          projekt.stop_device(device)
      else:
          return render(request, "admin/404.html")

      return redirect(f"/build_topology/devices/{vm}/{project}")

