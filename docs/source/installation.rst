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

   gnsave@server $ docker build -t gnsave .

Um die Installation abzuschließen muss man dann aus dem Image eine Container bauen

.. code-block:: console

   gnsave@server $ docker run -dit -p 80:80 --name gnsave_docker gnsave
   
   
Testung der Installation
----------------

.. code-block:: console

   gnsave@server $ curl -X GET http://localhost:80/


 
