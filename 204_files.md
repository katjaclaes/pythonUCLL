## Werken met text-files

### Files

Een programma zal data (in- en output) verwerken, in vele gevallen zal een programma data willen **bewaren** voor **later gebruik**.  
De eerste en meest directe manier om data op te slaan is door deze **data** naar een **file** te schrijven.  

Een file is in essentie:

* een **verzameling** van **bytes**
* opgeslagen op een **persistent medium** (harde schijf, usb-stick, ...)
* geadresseerd binnen **een filesysteem**
* met een specifiek **path** en **address**

Er bestaan verschillende soorten files:

* Text-files  
  Bevatten tekst-karakters die je kan lezen
* Executables  
  Bevatten code-instructies
* Media-files  
  Files die afspeelbare media (beelden, audio, video, ...) bevatten
* Andere binaire datafiles zoals spreadsheet-documenten, teksverwerkings-documenten, databases, ...
* ...
  
### Text-files

In dit deel gaan we leren werken met text-files.  

Text-files bevatten karakters (zoals we deze ook kennen van strings), karakters zijn bytes waarvan de waarde overeenstemt met een specifiek karakter.

### Werken met text-files in Python

#### Open en close

Werken met text-files start met het aanmaken van een file-object.
Dit file-object kan je aanmaken met de functie open() als volgt:  

~~~python
f = open("demofile.txt")
# Een aantal operaties...
f.close()
~~~

Na gebruik is het belangrijk dit file-object te sluiten met de operatie close.  
Het operating system kan namelijk de file locken voor gebruik vanuit andere programma's zolang dit file-object open staat.

#### Relatief vs absoluut

Vorig voorbeeld opende een file die in dezelfde directory staat als van waaruit je het python-programma uitvoert.
Je kan ook zeggen dat deze file **relatief** is aan het path waar je applicatie wordt uitgevoerd.

Als er een file in een subdirectory staat vanwaar je programma wordt uitgevoerd kan je een path beschrijven als volgt:

~~~python
f = open("subdirectory/demofile.txt")
# Een aantal operaties...
f.close()
~~~

Daarnaast als je een exact path (absoluut) wil beschrijven

~~~python
f = open("/home/bart/demofile.txt")
# Een aantal operaties...
f.close()
~~~

(en voor de Windows-gebruikers een plezier te doen)

~~~python
f = open("c:/users/bart/demofile.txt")
f.close()
~~~

#### Automatische close

Het probleem met bovenstaande code is dat als er een exceptie voordoet na open() het file-object mogelijk niet gesloten wordt.
Om dit te vermijden bestaat er de with-statement

~~~python
with open("demofile.txt") as f:
  print(f.read())
# Een aantal operaties...
~~~

Deze zal er voor zorgen dat - na het uitvoeren van de code binnen deze statement - het file-object zowiezo wordt gesloten (zelfs al is er een exceptie/crash)

#### Modes

Een eerste notie die je moet kennen is het gebruik van modes bij het openen van een file:

* "r" - Read (default)
* "x" - Create - maakt een file aan, en geeft een error wanneer deze file al bestaat
* "a" - Append - maakt een file aan als deze nog niet bestaat, alle writes zijn toevoegingen
* "w" - Write -  maakt een file aan als deze nog niet bestaat, overschrijft bestaande file

Deze mode kan je meegeven als een 2de (optioneel argument)

~~~python
with open("demofile.txt", "r") as f:
  print(f.read()) 
~~~

### Lezen uit een tekst-file 

Om te demonstreren hoe we met een text-file om kunnen gaan starten we met het aanmaken van een file genaamd **demofile.txt** met de volgende (nietszeggende) content:

~~~
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. 
Aenean commodo ligula eget dolor. Aenean massa. 
Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. 
Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. 
Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. 
Integer tincidunt. Cras dapibus. 
Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. 
Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. 
Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. 
Quisque rutrum. Aenean imperdiet. Etiam ultricies nisi vel augue. Curabitur ullamcorper ultricies nisi. Nam eget dui
~~~

#### Volledige inhoud uitlezen

Je kan de hele inhoud van een text-file opvragen via de read-functie.

~~~python
with open("demofile.txt", "r") as f:
  print(f.read()) 
~~~
Bovenstaande zal de volledige tekst afprinten (zoals hierboven).

Je kan je ook beperken tot het aantal bytes (in geval van tekstfiles de characters)

~~~python
with open("demofile.txt", "r") as f:
  print(f.read(5)) 
  print(f.read(5)) 
~~~

Bemerk ook dat de positie tot waar je al hebt gelezen wordt bijgehouden in het file-object

~~~
Lorem
 ipsu
~~~

#### Lijn per lijn lezen

Je kan ook kiezen om lijn per lijn uit te lezen.

~~~python
with open("demofile.txt", "r") as f:
  print(f.readline())
  print(f.readline()) 
~~~

Bovenstaande code zal de 2 eerste lijnen afdrukken.

~~~
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. 
Aenean commodo ligula eget dolor. Aenean massa.
~~~

#### Loopen door alle lijnen

Het file-object kan zich ook gedragen zoals een lijst van lijnen;  
Op dit object kan je dan een loop uitvoeren door de ganse file.

~~~python
with open("demofile.txt", "r") as f:
  for x in f:
    print(x) 
~~~

~~~
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. 

Aenean commodo ligula eget dolor. Aenean massa. 

Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. 

Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim.

...
~~~

### Schrijven naar een een file

Voor het schrijven naar een file zijn er 3 belangrijke modi die we moeten begrijpen:

* Een nieuwe file schrijven  => x
* Een bestaande file overschrijven => w
* Toevoegen aan het einde van een file => a

#### Een nieuwe file aanmaken

Het eerste scenario is dat we een nieuwe file willen aanmaken.  
In dit geval gebruiken we de modus **x**
* "x" - Create - maakt een file aan, en geeft een error wanneer deze file al bestaat

~~~python
with open("hello.txt", "x") as f:
  f.write("Dit is een nieuwe file!!!")
with open("hello.txt", "r") as f:
  print(f.read()) 
~~~

Als de file nog niet mocht bestaan zal er een nieuwe file hello.txt worden aangemaakt

~~~
$ python3 create_new_file.py
Dit is een nieuwe file!!!
$
~~~

Mocht deze file reeds bestaan, bijvoorbeeld door het programma een 2de maal te runnen zal er een exceptie worden opgeworpen door de open-functie

~~~
$ python3 create_new_file.py
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
FileExistsError: [Errno 17] File exists: 'hello.txt'
$
~~~

#### Nieuwe file of bestaande file overschrijven

Als we dezelfde code wijzigen om de modus **w** te gebruiken:

* zal er **geen error** worden opgeworpen als de **file reeds bestaat**
* maar wordt deze **overschreven**
* als deze toch **niet bestaat** wordt deze **aangemaakt**

Onderstaande code:

~~~python
with open("hello.txt", "w") as f:
  f.write("Dit is een nieuwe file!!!")
with open("hello.txt", "r") as f:
  print(f.read()) 

with open("hello.txt", "w") as f:
  f.write("De file is overschreven!!!")
with open("hello.txt", "r") as f:
  print(f.read()) 
~~~

* Zal de file eerst aanmaken (als deze nog niet bestaat)
* En vervolgens de inhoud overschrijven

~~~
$ python3 create_new_file.py
Dit is een nieuwe file!!!

De file is overschreven

$
~~~

#### Toevoegen aan het einde van de text-file

~~~python
with open("hello.txt", "w") as f:
  f.write("Dit is een nieuwe file!!!")
with open("hello.txt", "r") as f:
  print(f.read()) 

with open("hello.txt", "a") as f:
  f.write("Deze lijn is toegevoegd!!!")
with open("hello.txt", "r") as f:
  print(f.read()) 
~~~

~~~
$ python3 append_to_file.py
Dit is een nieuwe file!!!

Dit is een nieuwe file!!!
Deze lijn is toegevoegd!!!
$
~~~


### Andere file-operaties

Naast het lezen en schrijven van een file kan je ook nog andere operaties uitvoeren op files

#### Deleten van files

Het verwijderen van een file kan je via de functie remove.  
Hiervoor dien je wel de os-library te importeren

~~~python
import os
os.remove("hello.txt") 
~~~

Hou er natuurlijk rekening mee dat als de file niet bestaat deze code een error zal opwerpen:

~~~python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory: 'hello.txt'
~~~

#### Testen of de file bestaat

Deze exceptie kan je vermijden door na te gaan of deze file reeds betaat, die kan je met de exists()-functie
Zo kan je bovenstaande code verbeteren door de remove()-call af te schermen met een if-clausule

~~~python
import os
if os.path.exists("demofile.txt"):
  os.remove("demofile.txt")
else:
  print("The file does not exist") 
~~~

#### Zoeken in de file (direct vertaald uit py4e.com)

Wanneer u gegevens in een bestand doorzoekt, is het een veel voorkomend patroon om een bestand door te lezen, waarbij de meeste regels worden genegeerd en alleen regels worden verwerkt die aan een bepaalde voorwaarde voldoen. We kunnen het patroon voor het lezen van een bestand combineren met tekenreeksmethoden om eenvoudige zoekmechanismen te bouwen. 
Als we bijvoorbeeld een bestand willen lezen en alleen regels willen afdrukken die beginnen met het voorvoegsel "Van:", kunnen we de tekenreeksmethode startswith gebruiken om alleen die regels met het gewenste voorvoegsel te selecteren:

~~~python
with open('mbox-short.txt') as fhand:
    for line in fhand:
        if line.startswith('From:'):
            print(line)
~~~

De uitvoer ziet er geweldig uit, aangezien de enige regels die we zien de regels zijn die beginnen met "Van:", maar waarom zien we de extra lege regels? Dit komt door dat onzichtbare newline karakter. 
Elk van de regels eindigt met een nieuwe regel, dus de print statement drukt de tekenreeks af in de variabele regel die een nieuwe regel bevat en voegt vervolgens nog een nieuwe regel toe, wat resulteert in het dubbele spatiëringseffect dat we zien. We zouden line slicing kunnen gebruiken om alles behalve het laatste teken af te drukken, maar een eenvoudigere aanpak is om de rstrip-methode te gebruiken die witruimtes van de rechterkant van een string als volgt verwijdert:

~~~python
with open('mbox-short.txt') as fhand:
    for line in fhand:
        line = line.rstrip()
        if line.startswith('From:'):
            print(line)
~~~

Naarmate uw bestandsverwerkingsprogramma's ingewikkelder worden, wilt u misschien uw zoeklussen structureren met behulp van continue. Het basisidee van de zoeklus is dat u op zoek bent naar "interessante" regels en in feite "oninteressante" regels overslaat. En als we dan een interessante lijn vinden, doen we iets met die lijn. We kunnen de lus zo structureren dat het patroon van het overslaan van oninteressante regels als volgt verloopt:

~~~python
with open('mbox-short.txt') as fhand:
    for line in fhand:
        line = line.rstrip()
        #Skip de oninteressante regels
        if not line.startswith('From:'):
            continue
        #Print de interessante regels
        print(line)
~~~

De output van het programma is hetzelfde. In het Nederlands: de oninteressante regels zijn die die niet beginnen met "From:", die we overslaan door continue te gebruiken. Voor de "interessante" regels (d.w.z. regels die beginnen met "From:") voeren we de verwerking uit. 

We kunnen de find string gebruiken om een zoekopdracht in de teksteditor te simuleren die regels vindt waar de gezochte tekens zich ergens in de regel bevindt. Aangezien find zoekt naar het voorkomen van een tekenreeks binnen een andere tekenreeks en ofwel de positie van de tekenreeks retourneert als de tekenreeks gevonden is ofwel -1 als de tekenreeks niet is gevonden, kunnen we de volgende lus schrijven om regels weer te geven die de tekenreeks "@uct.ac.za" bevatten (d.w.z. ze komen van de Universiteit van Kaapstad in Zuid-Afrika)

~~~python
with open('mbox-short.txt') as fhand:
    for line in fhand:
        line = line.rstrip()
        if line.find('@uct.ac.za') == -1:
            continue
        print(line)
~~~


#### De gebruiker de bestandsnaam laten kiezen (direct vertaald uit py4e.com)

We willen echt niet elke keer onze Python-code moeten bewerken als we een ander bestand willen verwerken. Het zou bruikbaarder zijn om de gebruiker te vragen om elke keer dat het programma wordt uitgevoerd de bestandsnaam in te voeren, zodat ze ons programma op verschillende bestanden kunnen gebruiken zonder de Python-code te wijzigen. Dit is vrij eenvoudig te doen door de bestandsnaam aan de gebruiker te vragen als volgt:

~~~python
fname = input("Geef de volledige bestandsnaam: ")
with open(fname) as fhand:
    for line in fhand:
        line = line.rstrip()
        if line.find('@uct.ac.za') == -1:
            continue
        print(line)
~~~

We lezen de bestandsnaam van de gebruiker en plaatsen deze in een variabele met de naam fname en openen dat bestand. Nu kunnen we het programma herhaaldelijk op verschillende bestanden uitvoeren.
Voordat je naar het volgende gedeelte kijkt, kijk eens naar het bovenstaande programma en vraag jezelf af: "Wat kan hier mogelijk misgaan?" of "Wat zou onze vriendelijke gebruiker kunnen doen dat ervoor zou zorgen dat ons programma op onelegante wijze wordt afgesloten met een fout, waardoor we er niet zo cool uitzien in de ogen van onze gebruikers?"

#### Remember...try en except? (direct vertaald uit py4e.com)

Gebruikers zullen uiteindelijk alles doen wat ze kunnen om uw programma's te breken, hetzij per ongeluk of met kwade bedoelingen. In feite is een belangrijk onderdeel van elk softwareontwikkelingsteam een persoon of groep genaamd Quality Assurance (of kortweg QA) wiens taak het is om de gekste dingen te doen die mogelijk zijn in een poging de software te breken die de programmeur heeft gemaakt. 
Het QA-team is verantwoordelijk voor het vinden van de gebreken in programma's voordat we het programma hebben geleverd aan de eindgebruikers die de software mogelijk kopen of ons salaris betalen om de software te schrijven. Het QA-team is dus de beste vriend van de programmeur. 
Dus nu we de fout in het programma zien, kunnen we het elegant oplossen met behulp van de try/except structuur. We moeten ervan uitgaan dat het openen van het bestand kan mislukken en als volgt herstelcode toevoegen:

~~~python
fname = input("Geef de volledige bestandsnaam: ")
try: 
    with open(fname) as fhand:
        for line in fhand:
            line = line.rstrip()
            #Skip de oninteressante regels
            if line.find('@uct.ac.za') == -1:
                continue
            #Print de interessante regels
            print(line)
except:
    print('File cannot be opened:', fname)
    exit()
~~~

De exit() functie beëindigt het programma. 

Wanneer onze gebruiker (of QA-team) nu onnozelheden of slechte bestandsnamen intypt, "vangen" we ze en herstellen we ze gracieus!

### Meer info?

Er zijn nog vele mogelijkheden om files en directories te bewerken.  
Om deze te leren kennen kan je terecht bij https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files
