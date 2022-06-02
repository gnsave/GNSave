Userverwaltung
=====

.. _overview:

Überblick
------------

Die Userverwaltung basiert auf der schon in Django vorhandenen Userverwaltung. Sie verwaltet Benutzerkonten, Gruppen, Berechtigungen und Cookie-basierte Benutzersitzungen.


Usertypen
------------

In GNSave gibt es zwei Usertypen: Schüler und Lehrer. Die Lehreraccounts basieren auf dem Django Superuser und die Schüleraccounts auf den Django Usern.

Je nachdem welcher Typ der User ist hat werden ihm andere Funktionen freigeschaltet.

Jeder User hat einen Namen, ein Passwort, ein E-Mail und TYP.

Die folgenden Rechte sehen wie folgt aus:

.. image:: images/rechte.svg
  :width: 600
  :alt: rechte
  


Lehrer
^^^^^^^^^^^^

Lehrer haben grundsätzlich Zugriff auf alle Funktionen von GNSave. Das einzige worauf sie keinen Zugriff haben sind die privaten Dateien der Schüler.

.. image:: images/lehrer_overlay.png
  :width: 600
  :alt: lehrer

Schüler
^^^^^^^^^^^^

Schüler haben nur Zugriff auf ihre privaten und ihre Kursdateien.  

.. image:: images/schueler_overlay.png
  :width: 600
  :alt: schueler
  
User erstellen
----------------

Lehrer haben die Möglichkeit Schüler und andere Lehreraccounts zu erstellen.

Sie haben zwei Optionen wie sie das machen können.

Manuell
^^^^^^^^^^^^

Man kann schnell einzelne User per Textfeldeingabe erstellen.

.. image:: images/add_user_manuell.png
  :width: 600
  :alt: add_user_manuell

Mit einer File
^^^^^^^^^^^^

Wenn man eine große Anzahl von Usern erstellen will wird es schnell ziemlich Zeitintensiv jeden einzelnen manuell hinzuzufügen.

Als Lösung bieten wir die Funktion einen Schüler per File hinzuzufügen.

**Wichtig ist, dass die File mit .txt endet.**
   
.. image:: images/add_user_file.png
  :width: 600
  :alt: add_user_file
  
Die File könnte zum Beispiel so aussehen:

.. code-block:: text

    lorenz, gnsave123!, lorenz.bauer@htl.rennweg.at, user
    darius, gnsave123!, darius@htl.rennweg.at, user
    luther, gnsave123!, luther@htl.rennweg.at, user
    mateusz, gnsave123!, mateusz@htl.rennweg.at, user
    tino, gnsave123!, tino@htl.rennweg.at, user


   
Überblick der Features
----------------

To-Do

Diagramme
----------------

To-Do
