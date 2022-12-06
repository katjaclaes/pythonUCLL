## Synthese-oefening: Winkelmandje

Dit hoofdstukje bouwt rond een herhalings-oefening maken rond het werken met **klassen en objecten** gecombineerd met het gebruik van **lijsten**.

Naast het herhalen van het OO-principe willen we hier ook aantonen dat eender welk wat grotere applicatie **step-by-step** moet worden opgebouwd.  

Installeer python 3 via https://www.python.org/downloads/

Installeer volgende IDE https://thonny.org, we maken geen gebruik meer van repl.it om python files te maken maar stappen over naar de IDE Thonny.

Installeer vervolgens Git. Downloaden doe je hier: https://git-scm.com/downloads. Laat de standaardopties staan.

Maak gebruik van de git bash om git te configureren. Open git bash en geef volgende commando's in:

~~
> git config --global user.name "Jouw naam"
> git config --global user.email "Jouw mailadres"


### Step-by-step coderen (zeer belangrijk!!!)

Dit doe je door de volgende stappen constant te herhalen:

* **Coderen:** Een heel **kleine subset** van de **applicatie** opbouwen/toevoegen
* **Testen:**
    * Werkt je nieuwe functionaliteit?  
      Testen van je functie/code die je hebt gebouwd, ook soms **unit-testing** genoemd
    * Werkt de functionaliteit die je hebt toegevoegd?  
      Dit noemen ze ook **testen op regressie**
* **Revisioneren**
    * Eenmaal getest slaan we onze wijziging (step) op
    * We voegen een duidelijke commentaar toe
* ...en we starten opnieuw...

De laatste actie - revisioneren - is iets wat we nu voor de eerste maal introduceren.    
Het komt er op neer van (met behulp van een tool) de evolutie en verschillende versies bij te houden, waardoor dat je:

* Een historiek kan behouden van de wijzigingen van je code
* Kan terugkoppelen naar een vroegere specifieke revisie
* Code delen tussen verschillende personen (en zelfs organisaties)
* ...

De tool die we hiervoor gebruiken is **Git**, een quasi standaard op gebied van code-beheer

### Git: Aanmaken van een project

In dit voorbeeld gaan we Git gebruiken om de wijzigingen van onze applicatie bij te houden.  

We starten met:

* We **maken** een **folder** aan (we noemen deze **basket**)
~~
> mkdir basket

* **Navigeren** (in de command-line-prompt) naar deze folder
~~
> cd basket

* We voeren het commando **"git init"** uit binnen deze folder

~~~
Initialized empty Git repository in /Users/katja/basket/.git/
~~~

Deze actie maakt - in deze folder basket - een lokale **git-repository**.  
Zo'n git-repository is 

* Een soort van database waar je **code-wijzigingen** kan **bijhouden/traceren**
* Als een soort van **snapshot** (zoals je bijvoorbeeld een snapshot van een harde schijf zou nemen)
* Het stelt je in staat een historiek bij te houden en zelfs terug te keren naar een vorige **revisie**

De files die deze database omvatten bevinden zich in een verborgen folder **.git** .

Met het commando **"git status"** kan je controleren wat de status is.

~~~
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
~~~

De output van dit commit **suggereert** het gebruik van **git add** te gebruiken, we komen hier zo dadelijk nog op terug.

### Code schrijven: Basket-item-class

Alvorens met git verder te gaan starten we met **code te schrijven**.  
Bedoeling is dat we een **applicatie** gaan maken die een **winkelmandje** (of **winkellijstje**) gaat beheren.

Zo'n winkelmandje bestaat uit verschillende **items** die je in dat **mandje** mag droppen.  
Laten we starten met er van uit te gaan dat zo'n **item** een **beschrijving** en een **prijs** bevat...

We hebben in het studentenvoorbeeld gezien hoe je zulke gestructureerde data kan **bijhouden/groeperen** in een **klasse**.

We starten met een nieuwe file aan te maken in Thonny en voorzien daarin een klasse **BasketItem**:

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
	self.itemPrice = price
~~~

Deze klasse bevat **3 attributen**, een verwijzing naar zichzelf, een beschrijving en een prijs van het item. Bewaar dit bestand als **basket.py** in **dezelfde
directory** als die je aangemaakt hebt bij het maken van je repository in Git.

Om zeker te zijn van correctheid voeren we onze applicatie uit binnen thonny. Maak hiervoor gebruik van het groene "run" pijltje. Je kan het ook uitvoeren door 
volgend commando te gebruiken in de opdrachtprompt.

~~~
> python basket.py 
~~~

Vanzelfsprekend doet deze nog **niet** erg **veel**, daar komen we zo dadelijk **op** **terug**.  
Eerst gaan we echter onze eerste **code-wijzigen registereren/revisioneren**

### Git: Je 1ste commit met git...

We hebben ons **eerste stukje code** geschreven, als we via het git-commando **"git status"** de status opvragen...

~~~
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        basket.py

nothing added to commit but untracked files present (use "git add" to track)
~~~

...zien we dat git gezien heeft dat de file is gewijzigd en dat deze niet wordt getraceerd (tracked)   
We gebruiken het command **"git add <file>"** om deze toe te voegen aan de git-repository

~~~
$ git add basket.py 
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   basket.py
~~~

Er staat **"Changes to be committed"**, dit betekent dat je nu aan de **git-repo** hebt meegedeeld dat er een **wijziging** is.  
De wijziging is echter **nog niet** in de git-repo **opgeslagen**, om dit te volbrengen moeten we een **commit** uitvoeren.

Dit kan je met het commando **"git commit -m"**.  
Zo'n **commit** moet altijd vergezeld gaan van een boodschap, in dit geval "Creating class BasketItem.py".  

> Belangijk:  
> Probeer deze **boodschap** kort maar toch **duidelijk** te maken.  
> Hoe **duidelijker** deze is hoe **gemakkelijker achteraf** om te consulteren wat je wijziging waren.

~~~
$ git commit -m "Creating class BasketItem.py"
[master (root-commit) 6e8de93] Creating class BasketItem.py
 1 file changed, 4 insertions(+)
 create mode 100644 basket.py
$ git status
On branch master
nothing to commit, working directory clean 
$
~~~

Als we de status oproepen zien we dat er geen nieuwe wijziging meer is.  
Met het commando **"git log"** kan je dan zien dat je wijziging is geregistreerd

~~~
$ git log
commit 6e8de9336064b7c7b7ff1c5e3ebff40a068efb7b
Author: jouw gegevens
Date:   Sun Jan 10 19:43:15 2021 +0100

    Creating class BasketItem.py
$
~~~

Op de eerste lijn van deze output zie je lange string van **hexadecimale tekens** (6e8de9336064b7c7b7ff1c5e3ebff40a068efb7b), dit is wat we noemen de **commit-id**, een unieke **identifier** voor je code-wijzigingen

> **Belangrijk:**  
> Zo'n commit is het centrale begrip in git, het is een soort van snapshot van je code op een bepaald tijdstip


### Code schrijven: event-loop

We hebben nu echter **nog geen applicatie** daarvoor zijn er nog **2** belangrijke **elementen** nodig:

* Een **lijst** van BasketItem-objecten die kan worden bijgewerkt
* Een **event-loop** waar we de nodige acties implementeren

#### Lijst van BasketItem-objecten

De **eerste stap** is een **lijst** aanmaken als globale variabele waarin we BasketItems kunnen toevoegen en bewerken.

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
items = []
~~~

#### Event-loop (loop)

De applicatie moet natuurlijk nog wel iets doen, dus als **eerste stap** zetten we de **interactie met de gebruiker** op.  
Om met de gebruiker te praten voegen we:

* Een **oneindige lus** toe
* Waar we telkens **input** gaan vragen aan de gebruiker
* Als deze gebruiker antwoordt (**event**)
* Voeren we een **actie** uit 
* En geven we **feedback** aan de gebruiker

Zo'n loop is wat we noemen een **event-loop**, telkens als de gebruiker een ingave doet zal deze event-loop een reactie geven.

Een eerste versie van de loop...

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
items = []

while True:
	pass
~~~

Hier ontbreekt nog een stuk om van een event-loop te spreken...

> Het pass-statement wordt hier enkel tijdelijk gebruikt gezien we hier nog geen invulling hebben gegeven aan onze loop

#### Event-loop (menu)

Een **oneindige loop** is natuurlijk **niet voldoende**, de gebruiker moet een **menu** hebben (afgeprint).  
We printen hier het menu telkens af en vangen gebruikers-input op via de functie **input()**

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
items = []

menu = """
1> Voeg item toe
2> Print items af
3> Sluit af
"""

while True:
	menu_input = input(menu)
~~~

De **user-input** wordt gevraagd en **opgevangen**, maar er is nog **meer nodig**...

#### Event-loop (if-else)

We moeten er natuurlijk voor zorgen dat deze **user-input verwerkt** wordt.  
Hiervoor plaatsen we een **if/elif-clausule** voor elke **menu-optie**.

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
	
items = []
	
menu = """
1> Voeg item toe
2> Print items af
3> Sluit af
"""

while True:
    menu_input = input(menu)
    if menu_input == "1":
        print("TODO: Voeg item toe")
    elif menu_input == "2":
        print("TODO: Print item af")
    elif menu_input == "3":
        print("TODO: Sluit de applicatie af")
    else:
        print("Foutieve keuze")
~~~

Voorlopig printen we een **tijdelijke TODO-boodschap** waarmee we kunnen **testen** of onze event-loop correct werkt.   
We voeren even een **korte test** uit...

~~~
$ python basket.py 

1> Voeg item toe
2> Print items af
3> Sluit af
1
TODO: Voeg item toe

1> Voeg item toe
2> Print items af
3> Sluit af
4
Foutieve keuze

1> Voeg item toe
2> Print items af
3> Sluit af
~~~

...en zien dat de boodschappen worden afgeprint overeenkomstig de keuzes.  
Het **basis-skelet** van onze **event-loop** lijkt **ok** te zijn.  

### Git: Een 2de commit...

Een nieuwe fase van onze applicatie is **ontwikkeld** en **getest**, we gaan nu deze **code-wijziging** toevoegen aan onze **git-repo**.

Als we de status opvragen geeft git aan dat er een nieuwe wijziging is.  

~~~
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   basket.py

no changes added to commit (use "git add" and/or "git commit -a")
~~~

Wij hebben deze **wijziging** echter **nog niet klaargezet** voor de commit.  
Hiervoor gebruiken we opnieuw het commando **"git add"**

~~~
$ git add basket.py
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   basket.py
~~~

De status geeft nu aan dat deze kan **gecommit** worden.  
We doen dit opnieuw met een korte maar duidelijke boodschap.

~~~
$ git commit -m "Setup of basic event-loop and -menu"
[master ecc9bc7] Setup of basic event-loop and -menu
 1 file changed, 20 insertions(+), 1 deletion(-)
~~~

Merk op dat onze **git-historiek** nu ook **2** commits bevat

~~~
$ git log
commit ecc9bc7dea83661149a7c5bd9942f1b36c8d6e54
Author: jouw gegevens
Date:   Sun Jan 10 21:20:20 2021 +0100

    Setup of basic event-loop and -menu

commit 6e8de9336064b7c7b7ff1c5e3ebff40a068efb7b
Author: jouw gegevens
Date:   Sun Jan 10 19:43:15 2021 +0100

    Creating class BasketItem.py
~~~


### Code schrijven: programma/event-loop beëindigen

Tot nog toe moesten we ons eerste programma afsluiten met **ctrl+c**  
Het eerste event dat we al kunnen afwerken is **"3> Sluit af"** opdat we het programma op een elegante manier kunnen afwerken.

Hiervoor gebruiken we de python-functie **exit()** die er zal voor zorgen dat het programma wordt afgesloten.

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
items = []

menu = """
1> Voeg item toe
2> Print items af
3> Sluit af
"""

while True:
    menu_input = input(menu)
    if menu_input == "1":
        print("TODO: Voeg item toe")
    elif menu_input == "2":
        print("TODO: Print item af")
    elif menu_input == "3":
        print("Programma wordt beeindigd")
        exit()
    else:
        print("Foutieve keuze")
~~~

### git: nog commit's

We gaan deze wijziging ook **bewaren** in de git-repo.  

We **voegen** deze **commit toe**...

~~~
$ git add basket.py 
$ git commit -m "Implementing exit-event"
[master a29a73a] Implementing exit-event
 1 file changed, 2 insertions(+), 1 deletion(-)
~~~

Wanneer je een **git log** opvraagt zie je dat de **git-historiek** zich langzaam maar zeker begint **op te bouwen**

### Code schrijven: Afdrukken van items

We hebben bij een vorige commit een **lijst** gemaakt die wordt gebruikt om de **items** bij te houden.  

In **deze wijziging/commit** gaan we deze **lijst afdrukken**, gezien we echter de invulling nog niet hebben uitgewerkt maken we voorlopig een fake/hardcoded lijst aan:

> **Belangrijk:**  
> Het gebruik van deze fake data dient achteraf verwijderd te worden 
> maar het laat ons toe onze code-wijziging te testen.

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
items = []

menu = """
1> Voeg item toe
2> Print items af
3> Sluit af
"""
	
# Temporary list/will be removed later on
items.append(BasketItem("Laptop", 1000))
items.append(BasketItem("USB-stick", 10))

while True:
    menu_input = input(menu)
    if menu_input == "1":
        print("TODO: Voeg item toe")
    elif menu_input == "2":
        for item in items:
            print(item.description, "voor prijs", item.itemPrice)
    elif menu_input == "3":
        print("Programma wordt beeindigd")
        exit()
    else:
        print("Foutieve keuze")
~~~

Onder **optie 2** hebben we  een **loop** toegevoegd die deze **items afdrukt**.  

~~~
$ python basket.py 

1> Voeg item toe
2> Print items af
3> Sluit af
2
Laptop voor prijs 1000
USB-stick voor prijs 10

1> Voeg item toe
2> Print items af
3> Sluit af
3
Programma wordt beeindigd
$
~~~

Als we deze testen zien we dat de **hardcoded lijst** wordt **afgedrukt**, dus onze test is uitgevoerd dus we kunnen **revisioneren**


### git: ... volgende commit

We voegen onze **wijzigingen** toe aan de git repo met een commit:

~~~
$ git add basket.py
$ git commit -m "Printing the available items"
[master 07d49e9] Printing the available items
 1 file changed, 12 insertions(+), 1 deletion(-)
~~~ 

### Code schrijven: items toevoegen

Om er een **interactieve applicatie** van te maken moeten we **user-input** gebruiken om het **winkelmandje** aan te vullen.  
We doen dit door **event 1** te **implementeren** door de 3 volgende taken toe te voegen:

* Vraag **user-input** op (beschrijving en prijs)
* **Maak BasketItem-object** aan met input
* Voeg BasketItem-object toe aan **lijst**

> We verwijderen hierbij ook de eerder aangemaakte **hard-coded** lijst

~~~python
class BasketItem:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
items = []

menu = """
1> Voeg item toe
2> Print items af
3> Sluit af
"""

while True:
    menu_input = input(menu)
    if menu_input == "1":
        # Request input from user
        description = input("Geef beschrijving: ")
        price = int(input("Geef prijs: "))
        # Create and append new item
        items.append(BasketItem(description, price))
    elif menu_input == "2":
        for item in items:
            print(item.description, "voor prijs", item.itemPrice)
    elif menu_input == "3":
        print("Programma wordt beeindigd")
        exit()
    else:
        print("Foutieve keuze")
~~~

Als we dit uittesten:

~~~
$ python basket.py 

1> Voeg item toe
2> Print items af
3> Sluit af
1
Geef beschrijving: Laptop
Geef prijs: 1000

1> Voeg item toe
2> Print items af
3> Sluit af
1
Geef beschrijving: Harde schijf
Geef prijs: 200

1> Voeg item toe
2> Print items af
3> Sluit af
2
Laptop voor prijs 1000
Harde schijf voor prijs 200

1> Voeg item toe
2> Print items af
3> Sluit af
~~~

De test is uitgevoerd:

* We kunnen meerdere items **toevoegen**
* En deze nog altijd **afprinten**

### git: ... volgende commit

We **voegen** onze wijzigingen **toe** aan de **git** repo:

~~~
$ git add basket.py
$ git commit -m "Adding items to the basket"
[master 94df14f] Adding items to the basket
 1 file changed, 9 insertions(+), 11 deletions(-)
~~~ 

### Code schrijven: Voeg een attribuut quantity toe

In een winkelmandje dien je soms **meerdere items** van **hetzelfde product** bij te houden.  
Om dit op te lossen voegen we aan onze klasse BasketItem een **attribute quantity** toe

Hiervoor **voegen** we aan de **constructor** een **attribuut toe**...

> *Nota:*  
> Net zoals we eerder bij functies hebben gezien kan je attributen optioneel maken 
> door er een default waarde bij te plaatsen.  
> Als men dan deze waarde zou weglaten (bij aanroep van de constructor) krijgt dit attribuut
> deze default waarde

~~~python
class BasketItem:
    def __init__(self, description, itemPrice, quantity = 1):
        self.description = description
        self.itemPrice = itemPrice
        self.quantity = quantity
    
    def totalPrice(self):
        return self.itemPrice * self.quantity
~~~

... daarnaast voegen we een functie **totalPrice()** toe, hiermee bereken we de werkelijke prijs

Binnen de event-loop passen we dan de print aan zodat die niet de prijs van 1 item afdrukt maar de prijs van de totaal aantal items.

~~~python
class BasketItem:
    def __init__(self, description, price, quantity = 1):
        self.description = description
        self.itemPrice = price
        self.quantity = quantity
    
    def totalPrice(self):
        return self.itemPrice * self.quantity
    
    
items = []

menu = """
1> Voeg item toe
2> Print items af
3> Sluit af
"""


while True:
    menu_input = input(menu)
    if menu_input == "1":
        # Request input from user
        description = input("Geef beschrijving: ")
        price = int(input("Geef prijs: "))
        quantity = int(input("Geef hoeveelheid: "))
        # Create and append new item
        items.append(BasketItem(description, price, quantity))
    elif menu_input == "2":
        for item in items:
            print(item.quantity, "*", item.description, " = ", item.totalPrice())
    elif menu_input == "3":
        print("Programma wordt beeindigd")
        exit()
    else:
        print("Foutieve keuze")
~~~

Als we dit dan **uittesten** krijgen we volgende output

~~~
1> Voeg item toe
2> Print items af
3> Sluit af
1
Geef beschrijving: Laptop
Geef prijs: 1000
Geef hoeveelheid: 2

1> Voeg item toe
2> Print items af
3> Sluit af
2
2 * Laptop  =  2000

1> Voeg item toe
2> Print items af
3> Sluit af
3
Programma wordt beeindigd
~~~

Test OK, we kunnen vervolgen met onze commit...

### git: commit

~~~
$ git commit -m "Adding a quantity to BasketItem"
[master c4a19e5] Adding a quantity to BasketItem
1 file changed, 8 insertions(+), 3 deletions(-)
~~~

### Totaal van de items

Interessant om te weten als gebruiker is de **totaalwaarde** van deze items.  
Hiervoor voegen we een loop toe binnen **event 2**

~~~python
class BasketItem:
    def __init__(self, description, itemPrice, quantity = 1):
        self.description = description
        self.itemPrice = itemPrice
        self.quantity = quantity
    
    def totalPrice(self):
        return self.itemPrice * self.quantity

menu = """
1> Voeg item toe
2> Print items af
3> Sluit af
"""

items = []

while True:
    menu_input = input(menu)
    if menu_input == "1":
        # Request input from user
        description = input("Geef beschrijving: ")
        price = int(input("Geef prijs: "))
        quantity = int(input("Geef hoeveelheid: "))
        # Append new item
        items.append(BasketItem(description, price, quantity))
    elif menu_input == "2":
        sumOfItems = 0
        for item in items:
            print(item.quantity, "*", item.description, " = ", item.totalPrice())
            sumOfItems = sumOfItems + item.totalPrice()
        print("Totale waarde:", sumOfItems)
    elif menu_input == "3":
        print("Programma wordt beeindigd")
        exit()
    else:
        print("Foutieve keuze")
~~~

~~~
1> Voeg item toe
2> Print items af
3> Sluit af
1
Geef beschrijving: Laptop
Geef prijs: 1000
Geef hoeveelheid: 2

1> Voeg item toe
2> Print items af
3> Sluit af
1
Geef beschrijving: Harde schijf
Geef prijs: 250
Geef hoeveelheid: 3

1> Voeg item toe
2> Print items af
3> Sluit af
2
2 * Laptop  =  2000
3 * Harde schijf = 750
Totaal: 2750

1> Voeg item toe
2> Print items af
3> Sluit af
3
Programma wordt beeindigd
~~~

De test is geslaagd...

### git: volgend commit...

...We kunnen dit **committen**

~~~
$ git commit -m "Adding total-value"
[master 88f498e] Adding total-value
 1 file changed, 3 insertions(+)
~~~


### Eventuele extra: Error-handling: Vermijden van negatieve ingaves en opvangen van niet int-getallen

Tot nog toe hebben we geen controles uitgevoerd op negatieve waardes.  
We passen de volgende regels toe:

* Enkel een hoeveelheid toelaten > 0
* Enkel een prijs toelaten >= 0
	
Als we momenteel geen getal in voeren voor hoeveelheid of prijs zal de applicatie crashen.  
We zullen dit opvangen door een ValueError-exceptie.
Vergeet niet te committen!


	

	
	
