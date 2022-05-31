Willkommen zur GNSave Dokumentation!
===================================

**GNSave** ist eine Django App die den Netzwerktechnik Unterricht mit GNS3 erleichtern soll. 

Mithilfe der **GNS3 REST-API** (https://gns3-server.readthedocs.io/en/latest/) und **Telnet** ermöglicht GNSave die Remote-Administration von mehreren GNS3 VMs von einem zentralen Ort.

Außerdem bietet GNSave einen Weg für Schüler ihre GNS3 Projekte zu speichern und bietet außerdem die Möglichkeit nach einer Neuaufsetzung der PCs immernoch an den Projekten weiterarbeiten zu können.

Für mehr Informationen und Hilfe bei der Installation siehe Sektion :doc:`installation` Sektion 

.. note::

   This project is under active development.

Inhalte
--------
.. toctree::
   
   installation
   overview
   gns3-api
   website
   fileserver
   
Kompatibilität
-------------

Die Installation funktioniert auf jedem Python3 oder Docker fähigen Betriebssystem. GNSave benutzt Python in der Version 3.8 und Django in der Version 3.0. 
