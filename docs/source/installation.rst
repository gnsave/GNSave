Installation
=====

.. _installation:

Nur Django
------------

Um GNS3 zu installieren muss man zuerst einmal das GitLab Repository clonen

.. code-block:: console

   gnsave@server $ git clone https://gitlab.com/HTL-Rennweg/itp2021/gnsave.git
   
Danach muss man Python und die Python Libraries(z.B. Django) installieren

.. code-block:: console

   gnsave@server $ sudo apt-get install python3
   gnsave@server $ cd gnsave/GNSave
   gnsave@server $ pip3 install -r requirements.txt

Zu guter Letzt muss man die manage.py starten

.. code-block:: console

   gnsave@server $ python3 manage.py runserver 0.0.0.0:80
   
Dockerisiertes Django mit Apache2
----------------

Um GNS3 zu installieren muss man zuerst einmal das GitLab Repository clonen

.. code-block:: console

   gnsave@server $ git clone https://gitlab.com/HTL-Rennweg/itp2021/gnsave.git
   
Danach muss man die Docker Engine installieren

.. code-block:: console

   gnsave@server $ apt-get install docker
   
Danach muss man mithilfe der Dockerfile das GNSave Image installieren

.. code-block:: console

   gnsave@server $ cd gnsave
   gnsave@server $ docker build -t gnsave .

Um die Installation abzuschließen muss man dann aus dem Image eine Container bauen

.. code-block:: console

   gnsave@server $ docker run -dit -p 80:80 --name gnsave_docker gnsave
   
   
Testung der Installation
----------------

.. code-block:: console

   gnsave@server $ curl -X GET http://localhost:80/
   
   
   
   
Mögliche Fehler
----------------

Error processing tar file no space left on device
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Problem:**

Wenn man die Dockerfile ausführt wird folgender Error Code geworfen:

Error processing tar file(exit status 1): write ...: no space left on device
 
**Grund:** 

Es ist nicht genügend Speicherplatz für das Herunterladen der Images vorhanden. 

Nach Abschluss der Installation wird etwa 1 GB verfügbarer Speicherplatz für die Images benötigt.  Dies beinhaltet nicht den zwischenzeitlichen/temporären Speicherplatz, den Docker für verschiedene Schichten während der Installation benötigt. 

**Lösung:**

Führe den Befehl df /var/lib/docker/ aus, um den verfügbaren freien Speicherplatz anzuzeigen. 

Überprüfen Sie das Verzeichnis /var/lib/docker/ und weisen Sie genügend Speicherplatz zu, um die Installation durchzuführen.



 
