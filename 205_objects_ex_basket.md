Installeer python 3 via https://www.python.org/downloads/

Installeer volgende IDE https://thonny.org, we maken geen gebruik meer van repl.it om python files te maken maar stappen over naar de IDE Thonny.

Installeer vervolgens Git. Downloaden doe je hier: https://git-scm.com/downloads. Laat de standaardopties staan.

Maak gebruik van de git bash om git te configureren. Open git bash en geef volgende commando's in:

~~
$ git config --global user.name "Jouw naam"
$ git config --global user.email "Jouw mailadres"

      Testen van je functie/code die je hebt gebouwd, ook soms **unit-testing** genoemd
    * Werkt de functionaliteit die je hebt toegevoegd?  
    * Eenmaal getest slaan we onze wijziging (step) op
De tool die we hiervoor gebruiken is **Git**, een quasi standaard op gebied van code-beheer
~~
> mkdir basket

~~
> cd basket

* We voeren het commando **"git init"** uit binnen deze folder
Initialized empty Git repository in /Users/katja/basket/.git/
Met het commando **"git status"** kan je controleren wat de status is.
No commits yet
We hebben in het studentenvoorbeeld gezien hoe je zulke gestructureerde data kan **bijhouden/groeperen** in een **klasse**.
We starten met een nieuwe file aan te maken in Thonny en voorzien daarin een klasse **BasketItem**:
    def __init__(self, description, price):
        self.description = description
	self.itemPrice = price
Deze klasse bevat **3 attributen**, een verwijzing naar zichzelf, een beschrijving en een prijs van het item. Bewaar dit bestand als **basket.py** in **dezelfde
directory** als die je aangemaakt hebt bij het maken van je repository in Git.
Om zeker te zijn van correctheid voeren we onze applicatie uit binnen thonny. Maak hiervoor gebruik van het groene "run" pijltje. Je kan het ook uitvoeren door 
volgend commando te gebruiken in de opdrachtprompt.
> python basket.py 
We hebben ons **eerste stukje code** geschreven, als we via het git-commando **"git status"** de status opvragen...
We gebruiken het command **"git add <file>"** om deze toe te voegen aan de git-repository
Dit kan je met het commando **"git commit -m"**.  
 1 file changed, 4 insertions(+)
Author: jouw gegevens
De **eerste stap** is een **lijst** aanmaken als globale variabele waarin we BasketItems kunnen toevoegen en bewerken.
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
while True:
> Het pass-statement wordt hier enkel tijdelijk gebruikt gezien we hier nog geen invulling hebben gegeven aan onze loop
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
while True:
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
	
items = []
	
Een nieuwe fase van onze applicatie is **ontwikkeld** en **getest**, we gaan nu deze **code-wijziging** toevoegen aan onze **git-repo**.
Hiervoor gebruiken we opnieuw het commando **"git add"**
Author: jouw gegevens
Author: jouw gegevens
Hiervoor gebruiken we de python-functie **exit()** die er zal voor zorgen dat het programma wordt afgesloten.
    def __init__(self, description, price):
        self.description = description
        self.itemPrice = price
        
items = []
We gaan deze wijziging ook **bewaren** in de git-repo.  