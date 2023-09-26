# Steuerung der Roboterendeffektorlage mithilfe eines neuroevolutionär trainierten neuronalen Netzes

Dieses Repository befasst sich mit der Positions- und Orientierungssteuerung eines Roboterendeffektors. Dabei wurden mit zwei verschiedenen Jupyter Notebooks neuronale Netze generiert die Position oder Orientierung steuern können. Bei der Orientierung gibt es leider Probleme da bei der Orientierungsdarstellung mit Quaternionen die Fitnessfunktion nicht eindeutig identifizieren kann welche Änderung der Orientierung ein besseres Ergebnis liefert. Aus diesem Grund sind im Notebook zur Orientierung lediglich Versuche die fehlgeschlagen sind. Sie können allerdings als Ansatz für weitergehende Projekte genutzt werden. Die Arbeit selber basiert auf einer Abschlusarbeit zum Thema *Erstellen eines neuronalen Netzes zur Steuerung eines Roboterarmes durch neuronevolutionäre Algorithmen*, weshalb bei ungeklärten oder unerklärten Dateien [hier](https://github.com/PIX3LFLUX/NeuRobotics) nachgelesen werden kann.

## Pakete

Um das Repository vollständig zu nutzen, müssen folgende Packages installiert werden:
+ numpy
+ neat-python
+ pybullet
+ pyquaternion
+ graphviz

Diese können mit den Befehlen: 

```sh 
pip install numpy
pip install neat-python
pip install pybullet
pip install pyquaternion
pip install gaphviz
``` 

installiert werden. Falls Probleme beim Installieren auftreten oder genauere Details zu den Packages erwünscht sind, gibt es für [neat](https://github.com/CodeReclaimers/neat-python), [pyquaternion](https://github.com/KieranWynn/pyquaternion) und [pybullet](https://github.com/bulletphysics/bullet3) bereits bestehende Repositorys.

## Notebooks

Dieses Repository besteht aus 5 Jupyter-Notebooks. Das Notebook RoboterBewegen.ipynb ermöglicht es dem Nutzer den Roboter zu Steuern. Dabei kann jedes Robotergelenk einzeln bewegt werden. Die benötigten Tasten für jedes Gelenk stehen im Code kommentiert. 

Das zweite Notebook ist CreatePositins.ipynb. Dieses ist die Grundlage für die beiden Evolutionsnoteboks, da hier Roboterlagen bestimmt und gespeichert werden welche vom Roboter angefahren werden können. Ist eine Position außerhalb  der Reichweite des Roboters oder sorgt für eine Selbstkollision des Roboters wird sie nicht für das darauf aufbauende Notebook benutzt.

Das dritte und vierte Notebook sind OrientierungEvolution.ipynb und PositionEvolution.ipynb diese sind Hauptbestandteil dieser Arbeit. Diese nutzen die in CreatePositions erzeugten Roboterlagen, um mit dem NEAT-Algorithmus Netze zu entwickeln die je nach Notebook die Position oder Orientierung des Roboterendeffektors richtig einstellen. Das heißt dass der Roboter am Ende der Evolution möglichst nah an der Zielposition ist oder sehr nah an der vorgegebenen Orientierung. Im Orientierungsnotebook sind verschieden Ansätze kommentiert, man kann beispielsweise verschieden Distanzmaße benutzen (in der Funktion calcOrDistance) oder auch verschiedene Funktionen zur Berechnung des Scores benutzen (Kommentiert in fitnessFunction3). Ebenso ist im Programm ein Ansatz der Novelty Search auskommentiert. 

Das Letzte Notebook Netz-Test.ipynb ist zum Testen des Ergebnisses der Evolution. Das Netz, welches am Ende der Evolution gespeichert wird kann in diesem Programm als Input angegeben werden. Dieses Netz wird dann 100 Zielpunkte anfahren und die Distanz zum Zielpunkt ermittelt. Anschließend gibt es dann eine Auswertung welche anzeigt in welchem Wertebereich die Distanzen zu den Zielpunkten lagen.

## Benutzung des Repositorys
1.	Diese Repository Klonen.
2.	Die Packages wie oben im Abschnitt benötigte Packages installieren.
3.	Einmal das CreatePositions Notebook ausführen. Dabei darauf achten, dass je nach Anwendung nicht alle Teile des Programms nötig sind.
4.	Nun kann die entsprechende Config Datei (config_or für die Orientierung, config_pos für die Position) angepasst werden damit der NEAT-Algorithmus so arbeitet wie erwünscht. 
5.	Wenn alle vorherigen Schritte durchgeführt wurden, kann nun das Evolutions-Notebook ausgeführt werden. Dabei kann zwischen verschiedenen Fitnessfunktionen gewählt werden. Bei der Orientierung gibt es auch verschiedene Distanzmaße, die getestet werden können.
6.	Um nun die Qualität des Netzes zu testen kann nun das gespeicherte Netz im Notebook Netz-Test reingeladen werden und die Präzision von diesem ermittelt werden.


