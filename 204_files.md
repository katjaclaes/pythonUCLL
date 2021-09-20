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

#### Verwijderen van een directory

Om een directory te verwijderen dien je de rmdir()-functie te gebruiken

~~~python
import os
os.rmdir("a_folder") 
~~~

Let wel, deze zal falen 

* als de directory niet bestaat 

~~~
...
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory: 'a_folder'
>>> 
~~~

> Om dit te vermijden kan je os.path.exists() gebruiken)

* Als de directory niet leeg is

~~~
...
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
OSError: [Errno 39] Directory not empty: 'a_folder'
~~~

### Verdere info

Er zijn nog vele mogelijkheden om files en directories te bewerken.  
Om deze te leren kennen kan je terecht bij https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files
