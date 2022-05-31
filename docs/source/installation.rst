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

   gnsave@server $ cd gnsave 
   gnsave@server $ sudo apt-get install python3
   gnsave@server $ pip3 install -r requirements.txt
   
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

   gnsave@server $ cd docker
   gnsave@server $ docker build -t gnsave/GNSave .

Um die Installation abzuschließen muss man dann aus dem Image eine Container bauen

.. code-block:: console

   gnsave@server $ docker run -dit -p 80:80 gnsave/GNSave gnsave_docker
   
   
Testung der Installation
----------------

.. code-block:: console

   gnsave@server $ curl -X GET http://localhost:80/

.. toctree::
   :hidden:
   
   installation
   overview
   gns3-api
   website
   fileserver

 
