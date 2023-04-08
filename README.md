# Projektseite-2
Das Pizzeria-Spiel von Paula Miltsch und Juliane Reimpell

## Inhaltsverzeichnis
- [Spielidee](https://github.com/InformatikUnterrichtJ/Projektseite-2/blob/main/README.md#spielidee)
- [Warum wir uns für Python entschieden haben](https://github.com/InformatikUnterrichtJ/Projektseite-2/blob/main/README.md#warum-wir-uns-f%C3%BCr-python-entschieden-haben)
- [Aufbau des Spiels](https://github.com/InformatikUnterrichtJ/Projektseite-2/blob/main/README.md#aufbau-des-spiels)
- [Fazit](https://github.com/InformatikUnterrichtJ/Projektseite-2/blob/main/README.md#fazit)


### Spielidee
Die Idee war ein Spiel zu entwickeln bei dem man eine Pizzeria besitzt und seine Kunden bedient, die aus einer Auswahl Pizzen bestellen. "Bedienen" sollte in diesem Fall bedeuten, dass man die Pizza, je nachdem welche art bestellt wurde, mit den passenden Zutaten zubereitet.
Die Bestellung erschein in einer Sprechblase in der rechten unteren Ecke des Fensters und beinhaltet den Namen der zu erstellenden Pizza. Der Spieler wählt dann die entsprechenden Zutaten aus der Reihe am oberen Rand des Fensters aus und zieht diese auf die Arrbeitsfläche. Auskunft über die zu kombinierenden Zutaten gibt eine Karte. Sind alle Zutaten richtig auf der Arbeitsfläche kombiniert, so wird eine neue Bestellung generiert und der Spieler muss erneut die Zutaten zusammenfügen.

### Warum wir uns für Python entschieden haben
Nachdem wir uns beim letzten Mal für Scratch entschieden hatten und dies ein Block-Programmiersystem ist, mussten wir uns für diese Projekt neu orientieren. Da uns durch den ersten Versuch von physical computing immernoch bewusst war, dass wir nicht mit Arduino arbeiten wollen, haben wir uns nach Programmiersprachen für Computerspiele umgeschaut. Dabei sind wir schnell auf Java gestoßen, doch empfunden wir dieses als sehr unübersichtlich und wussten nicht genau wo wir anfangen sollen. Bei der Recherche über Java fiel uns dann Python in Kombination mit PyGame in die Arme. PyGame erschien uns weit aus schlüssiger und im Internet haben wir schnell hilfrecihe Tutorials gefunden. Auch erschien es uns geeignet, da es Funktionen wie eine Zufallsauswahl besitzt und es möglich ist eigene Bilder als Spielfiguren einzusetzen, sowie eine Maussteuerung zu programmieren.

### Aufbau des Spiels
Das Spiel besteht aus dem Aufbau des Fensters, der Hauptschleife des Spiels, der Bestellung und den Spielfiguren, beziehungsweise den Zutaten. Der Code der einzelnen Spielfiguren ähnelt sich, da sie alle eine sehr ähnliche Funktionen erfüllen.

Damit überhaupt mit den Begriffen von Python und PyGame gearbeitet werden kann, müssen diese zuerst installiert werden. Der Code beginnt also mit dieser Installierung.

```ruby
import pygame
import random
```
Es folgt die Festlegung von Variablen wie beispielsweise die Frames per second (FPS) und die Farben Schwarz und Weiß. Da wir mir Bildern zur Darstellung vom Hintergrund und den Spielfiguren arbeiten, müssen keine weiteren Farben definiert werden. Außerdem wird die Variable "spielaktiv" erstellt und als wahr befunden. Diese wird später genutzt um das Spiel an geeigneter Stelle zu beenden. Zusätzlich wird noch ein Zähler eingesetzt, der Später dafür genutzt wird falsche Bestellungen zu erkennen und mit dem Satz "Der Kunde ist unzufrieden" in der Sprechblase zu reagieren. Darüberhinaus wird eine Schriftart für das Spiel definiert und diese den später in einer Sprechblase erscheinenden Pizzanamen und auch dem Satz "Der Kunde ist unzufrieden" zugeordnet, damit diese später auch in der entsprechenden Schrift erscheinen. Wir haben uns hierbei für "Comic Sans MS" entschieden.
Zusätzlich müssen die Variabeln, die später angeben, dass ein Item bewegt wird, als falsch, also als inaktiv deklariert werden. Des Weiteren wird an dieser Stelle auch die Bestellung, als eine Zufallsgenererierung der Zahlen eins bis vier, erstellt.

```ruby
pygame.init()
W, H = 1200, 800
FPS = 100
SCHWARZ = (0, 0, 0)
WEISS = (255, 255, 255)
spielaktiv = True
my_font = pygame.font.SysFont('Comic Sans MS', 30)
MozarellaSurf = my_font.render('Mozarella Pizza',False,(0, 0, 0))
SalamiSurf = my_font.render('Salami Pizza',False,(0, 0, 0))
FunghiSurf = my_font.render('Funghi Pizza',False,(0, 0, 0))
MargheritaSurf = my_font.render('Margherita Pizza',False,(0, 0, 0))
FalschSurf = my_font.render('Der Kunde ist unzufrieden', False, (255, 0, 0))

Bestellung = random.randint(1,4)
FalschZähler = 0

TeigAktiv = False
BasilikumAktiv = False
PilzAktiv = False
KäseAktiv = False
SalamiAktiv = False
TomatensauceAktiv = False
MozarellaAktiv = False
```
Nun muss der Hintergrund des Fensters bestimmt werden. Hierzu haben wir ein Bild ausgewählt und mit diesem das ganze Fenster ausgefüllt. Zum Hintergrund gehört ebenfalls noch die Arbeitsfläche, die ebenfalls als BIld platziert wird, jedoch nur als eine Teilfläche des Fensters. Platziert werden die Bilder auf dem bereits im Hintergrund existierendem Koordinatensystem, welches ebenfalls die Skalierung ermöglicht. Als Letztes wird noch die Sprechblase zum Hintergrund hinzugefügt. Diese ist ebenfalls ein eingesetztes Bild.

```ruby
Hintergrundbild = pygame.image.load("images/Hintergrundbild.jpg")
Hintergrundbild = pygame.transform.scale(Hintergrundbild,(1200, 800))
Holzbrett = pygame.image.load("images/Holzbrett.jpg")
Holzbrett = pygame.transform.scale(Holzbrett,(400, 350 ))
HolzbrettRect = Holzbrett.get_rect()
HolzbrettRect = HolzbrettRect.move(600, 400)
Sprechblase = pygame.image.load("images/Sprechblase.png")
Sprechblase = pygame.transform.scale(Sprechblase,(300,250))
SprechblaseRect = Sprechblase.get_rect()
SprechblaseRect = SprechblaseRect.move(0,500)
```
Es folgen die Spielfiguren. Für diese wird zuerst das jeweilige Bild eingesetzt und anschließend werden sie alle auf die Größe 200x200 verkleinert. Anschließend wird festgelegt wie die Spielfiguren reagieren sollen, wenn mit ihnen interagiert wird. Hierbei wird festgelegt, dass die Spielfiguren sich zuerst kopieren, damit sie in der oberen Zutatenzeile erhalten bleiben und anschließend bei einer zugeordneten Position auf der Arbeitsfläche beliben, wenn diese dort hin bewegt werden. Der Code der Zutaten unterscheidet sich dehalb nur an den Koordinaten des Platzes auf der Arbeitsfläche und des Platzes in der Zutatenzeile.

```ruby
Teig = pygame.image.load("images/TeigT.png")
Teig = pygame.transform.scale(Teig,(200, 200))
TeigRect = Teig.get_rect()
TeigRect2 = TeigRect.copy()
TeigRect3 = TeigRect.move(600,400)

Basilikum = pygame.image.load("images/BasilikumT.png")
Basilikum = pygame.transform.scale(Basilikum,(200, 200))
BasilikumRect = Basilikum.get_rect()
BasilikumRect2 = BasilikumRect.copy()
BasilikumRect3 = BasilikumRect.move(700,400)
BasilikumRect = BasilikumRect.move(200,0)

Pilz = pygame.image.load("images/PilzT.png")
Pilz = pygame.transform.scale(Pilz,(200, 200))
PilzRect = Pilz.get_rect()
PilzRect2 = PilzRect.copy()
PilzRect3 = PilzRect.move(750,500)
PilzRect = PilzRect.move(350,0)

Käse = pygame.image.load("images/KäseT.png")
Käse = pygame.transform.scale(Käse,(200, 200))
KäseRect = Käse.get_rect()
KäseRect2 = KäseRect.copy()
KäseRect3 = KäseRect.move(800,400)
KäseRect = KäseRect.move(500,0)

Salami = pygame.image.load("images/SalamiT.png")
Salami = pygame.transform.scale(Salami,(200, 200))
SalamiRect = Salami.get_rect()
SalamiRect2 = SalamiRect.copy()
SalamiRect3 = SalamiRect.move(800,500)
SalamiRect = SalamiRect.move(650,0)

Tomatensauce = pygame.image.load("images/TomatensauceT.png")
Tomatensauce = pygame.transform.scale(Tomatensauce,(200, 200))
TomatensauceRect = Tomatensauce.get_rect()
TomatensauceRect2 = TomatensauceRect.copy()
TomatensauceRect3 = TomatensauceRect.move(600,600)
TomatensauceRect = TomatensauceRect.move(800,0)

Mozarella = pygame.image.load("images/MozarellaT.png")
Mozarella = pygame.transform.scale(Mozarella,(200, 200))
MozarellaRect = Mozarella.get_rect()
MozarellaRect2 = MozarellaRect.copy()
MozarellaRect3 = MozarellaRect.move(800,600)
MozarellaRect = MozarellaRect.move(950,0)
```
Damit das Spiel nicht nach einer Bestellung vorbei ist muss der Wiederherstellungsbegriff ("reset()") definiert werden. Dieser soll später bewirken, dass das Spiel in die Ausgangslage zurück geht und eine neue Bestellung generiert. Für den Spieler beginnt an dieser Stelle das Spiel quasi erneut. Um auf die Ausgangslage zurück zu kommen müssen die Zutaten ganau wie zu Beginn des Spiels inaktiv gestellt werden. Damit dies bei einem Reset für den gesammten Code gilt und nicht nur für den Abschnitt indem sich der Ausdruck befindet müssen diese zuerst von einer lokalen zu einer globalen Variable abgeändert werden.

```ruby
def reset():
    global TeigAktiv
    global BasilikumAktiv
    global PilzAktiv
    global KäseAktiv
    global SalamiAktiv
    global TomatensauceAktiv
    global MozarellaAktiv
    global Bestellung
    TeigAktiv = False
    BasilikumAktiv = False
    PilzAktiv = False
    KäseAktiv = False
    SalamiAktiv = False
    TomatensauceAktiv = False
    MozarellaAktiv = False
    Bestellung = random.randint(1, 4)
 ```
 Bevor die Hauptschleife endlich beginnen kann muss nun noch das Fenster indem das Spiel laufen wird erstellt werden. Da die Höhe und Weite bereits definiert worden, wird nun ein Fenster mit dieser Größe erstellt. zusätzlich wird diesem die Caption "Pizzeria" zugeordnet und die Zeit gestartet, damit die Frames per seconds eingessetzt werden können. Außerdem wird noch mit dem Ausdruck ```pygame.display.flip()``` ermöglicht, dass Teile des Fensters einzelnt aktualisiert werden können.
 ```ruby
 fenster = pygame.display.set_mode((W, H))
pygame.display.set_caption("Pizzeria")
clock = pygame.time.Clock()

pygame.display.flip()
    clock.tick(FPS)
```
    
 #### Hauptschleife
 Die Hauptschleife definiert den tatsächlichen Ablauf des Spiels und besteht aus vielen if- und elif-Schleifen. Beginnen tut sie mit der Aussage während die Variable spielaktiv wahr ist, soll alles folgende passieren. Somit kann über die Variable spielaktiv das Spiel später beendet werden.
 Bevor die Fallbedingungen der Schleife, die später das Verhalten in besetimmten Events bestimmen, beginnen wird zuerst noch geprüft, ob der FalschZähler größer als null ist, also eine Bestellung falsch war. Ist dies der Fall wird mit -1 vom Ausgangswert runtergezählt, bis dieser wieder bei Null ist.
 Die erste Fallbedingung widmet sich den Keyboardtasten. Sie besagt, dass wenn im Fall das eine Taste gedrückt wurde diese die Escapetaste war, die Variable spielaktiv deaktiviert wird und folglich das Spiel beendet wird oder wenn im Fall das eine Taste gedrückt wurde diese die Entertaste war, die Bestellungen, je nachdem welche nummer ausgewählt wurde, darauf geprüft werden, ob die richtigen Zutaten aktiv sind, also die Zutaten richtig ausgewählt worden. Ist dies der Fall gibt es einen Reset. Sollten jedoch falsche Zutaten ausgewählt worden sein und die Bestellung ist nun fehlerhaft, so wird der FalschZähler auf 250 gesetzt. Die Zahl 250 wurde deshalb gewählt, da es mit einem FPS von 100 genau zwei einhalb sekunden braucht, um von dort mit -1 runterzuzählen.
 ```ruby
 
while spielaktiv:
    if FalschZähler > 0:
        FalschZähler = FalschZähler - 1
    for event in pygame.event.get():
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                spielaktiv = False
            elif event.key == pygame.K_RETURN:
                #Bestellung wird abgeschlossen
                if Bestellung == 1 and TeigAktiv == True and MozarellaAktiv == True and TomatensauceAktiv == True and BasilikumAktiv == True and KäseAktiv == False and PilzAktiv == False and SalamiAktiv == False:
                    #Bestellung richtig gemacht
                    reset()
                elif Bestellung == 2 and TeigAktiv == True and MozarellaAktiv == False and TomatensauceAktiv == True and BasilikumAktiv == False and KäseAktiv == True and PilzAktiv == False and SalamiAktiv == True:
                    reset()
                elif Bestellung == 3 and TeigAktiv == True and MozarellaAktiv == False and TomatensauceAktiv == True and BasilikumAktiv == False and KäseAktiv == True and PilzAktiv == True and SalamiAktiv == False:
                    reset()
                elif Bestellung == 4 and TeigAktiv == True and MozarellaAktiv == False and TomatensauceAktiv == True and BasilikumAktiv == False and KäseAktiv == True and PilzAktiv == False and SalamiAktiv == False:
                    reset()
                else:
                    reset()
                    FalschZähler = 250
```
### Fazit
