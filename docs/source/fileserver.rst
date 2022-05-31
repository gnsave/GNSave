Fileserver
=====

.. _fileserver:

Überblick
------------

Der Fileserver basiert auf einem Kurs System. Die User haben jedoch keine Rechte sondern entweder die Schüler oder die Lehrer Rolle. Je nach Accounttyp sieht der User dann andere Sachen. Lehrer haben zum Beispiel Zugriff auf das Cloning Tool und Schüler nicht.

Filesystem
------------

Das Filesystem ist in private und Kurs Dateien geteilt. Auf die privaten Dateien hat nur der jeweilige User Zugriff. Auf die Kurs Dateien hat wieder jeder Schüler nur auf seine eigenen Dateien Zugriff, aber der Kursleiter/Lehrer kann jegliche Schülerdateien einsehen.

Die Dateien auf die Lehrer Zugriff hat könenn so aussehen (er hat in jedem Folder alle Rechte):

.. image:: images/lehrer.svg
  :width: 600
  :alt: lehrer
 
Im Kontrast dazu sind das zum Beispiel die Dateien die ein Schüler sieht(grau heißt er kann nichts verändern):

.. image:: images/schüler.svg
  :width: 600
  :alt: schüler


Aufbau
------------

Das Filesystem ist dann logisch in zwei Teile geteilt. In die User und die Course Files

::
    files
    ├── users
    │   ├── lorenz
    │   │   └── project.gns3project
    │   │
    │   └── arthur
    │      └── plf_vorbereitung.gns3project
    │
    ├── courses      
    │   ├── 21-22-4AX
    │   │   └── plf_uebung.gns3project
    │   │   └── lorenz
    │   │   └── arthur
    │   │      └── plf_uebung.gns3project
    │   │ 
    │   └── 22-23-5AX
    │       └── matura_uebung.gns3project
    │       └── arthur
    │          └── matura_uebung.gns3project

.. image:: images/filesystem.svg
  :width: 800
  :alt: schüler


To-Do
   
Verwendete Module
----------------

To-Do
   
   
Überblick der Features
----------------

To-Do

 
