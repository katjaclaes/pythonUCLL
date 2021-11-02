## Errors en excepties

### Syntax-error

Het uitvoeren van Python-code gebeurt in 2 fases:

* **Parsen en interpreteren** van de Python-code
* Het eigenlijke **uitvoeren**

Als er **fouten** in de **code-syntax** zitten, kan dit **geweten** zijn bij de **start** van het **programma**  
Bijvoorbeeld bij volgende code vergeten we een ":"

~~~python
a = [1,2,3,4,5,6,7]
print("From 1 until 7")
for i in a
	print(i)
~~~

Als gevolg herkent de Python-interpreter de error en wordt er geen code uitgevoerd.

~~~
  File "test.py", line 2
    for i in a
             ^
SyntaxError: invalid syntax
~~~

### Programma wordt niet uitgevoerd

Hoewel de print-statement - "From 1 until 7" - voor de error voorkomt wordt deze niet uitgevoerd.  
Dit is omdat de Python-interpreter de volledige code inlaadt en nakijkt alvorens deze uit te voeren.  
Als er dan een fout in de file is geplaatst wordt de volledige code niet uitgevoerd.

### Runtime error

Er kunnen echter ook errors gebeuren "at runtime" zoals bijvoorbeeld

* Een functie-call die niet bestaat (functies komen nog aan bod later in de cursus)
* Een string die niet kan worden omgezet
* Delen door 0

Bijvoorbeeld...

~~~python
print("Hello")
a = 5/0
print(a)
~~~

...veroorzaakt

~~~
Hello
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
~~~

In dit geval zien we dat er ook duidelijk een **error** wordt aangegeven, in dit geval een ZeroDivisionError

### Een exceptie stopt het programma

Belangrijk in bovenstaande code, is dat voorgaande code (afprinten van hello) **wel** wordt **uitgevoerd**.

Het programma start wel degelijk maar stopt bij het aangegeven punt van error.

In tegenstelling tot een syntax-error kan een python-programma niet bij het parsen van de python-code bepalen dat er een error is.

### Excepties afvangen

Je kan in je code ervoor zorgen dat deze excepties worden **afgevangen** zonder dat ze het programma beeindigen.

Dit kan via een **try-block** in combinatie met een **except-block**.  
In onderstaande code proberen we een variabele af te printen die niet bestaat.  

~~~python
print("Begin programma")
try:
  print(x)
  print("Na de error")
except:
  print("An exception occurred")
print("Einde programma")
~~~

We kunnen dit doen aan de hand van een default except-block, deze gaat eender welke error (buiten SyntaxError) afvangen.

Dit heeft volgende uitvoering als resultaat...

~~~
Begin programma
An exception occured
Einde programma
~~~

We zien hier dat:

* Het programma wordt uitgevoerd
* De try-block wordt onderbroken (bij print(x))
* De except wordt uitgevoerd
* De code verder loopt na de except

### Excepties opvangen per type

Je kan ook het **type van exceptie aangeven** dat je wil afvangen.  
In dit geval beperk je het opvangen tot een specifieke error, de NameError.

~~~python
print("Begin programma")
try:
  print(x)
  print("Na de error")
except NameError:
  print("An exception occurred")
print("Einde programma")
~~~

Het volstaat hier het type te definiëren na het except-keyword.

Als je echter een andere error genereert (bijvoorbeeld een ZeroDivisionError)...

~~~python
print("Begin programma")
try:
  print(5/0)
  print(x)
  print("Na de error")
except  NameError:
  print("An exception occurred")
print("Einde programma")
~~~

...zal dit echter niet worden afgevangen...

~~~
ZeroDivisionError: integer division or modulo by zero
~~~

...en wordt het programma beeindigd (de prints daarna worden niet afgedrukt)

### Meerdere except-blokken

Om dit probleem te verhelpen - en meerdere excepties op te vangen - kan je meerdere except-blocks plaatsen.  
Met onderstaande except-block op ZeroDivisionError te plaatsen vermijd je dat het programma wordt beeindigd.

~~~python
print("Begin programma")
try:
  print(5/0)
  print(x)
  print("Na de error")
except  NameError:
  print("A NameError-exception occurred")
except  ZeroDivisionError:
  print("A ZeroDivision-exception occurred")
print("Einde programma")
~~~

Je kan ook de de **default** except-block hier aan toevoegen

~~~python
print("Begin programma")
try:
  print(5/0)
  print(x)
  print("Na de error")
except  NameError:
  print("A NameError-exception occurred")
except  ZeroDivisionError:
  print("A ZeroDivision-exception occurred")
except:
  print("Another error")
print("Einde programma")
~~~

In dat geval zullen alle errors worden afgevangen (maar de boodschap zal verschillen in geval van NameError of ZeroDivisionError)


### else-clausule

Je kan ook een else-clausule toevoegen, deze zal **enkel** worden uitgevoerd als er zich geen error heeft voorgedaan.

~~~python
try:
  print("Hello")
except:
  print("Something went wrong")
else:
  print("Nothing went wrong")
~~~

### finally

Je kan nog een extra tak toevoegen aan een try constructie, namelijk **finally**. Bij finally kan je een serie statements opnemen die worden uitgevoerd ongeacht de wijze waarop de try constructie wordt verlaten. Als alles normaal verloopt, worden de statements bij de finally uitgevoerd, maar ook als je een runtime error krijgt, worden ze uitgevoerd. Je kunt bijvoorbeeld finally gebruiken om er zeker van te zijn dat een bestand dat je geopend hebt, wordt gesloten.

~~~python
try:
  f = open("demofile.txt")
  f.write("Lorum Ipsum")
except:
  print("Something went wrong when writing to the file")
finally:
  f.close() 
~~~

### Zelf excepties opwerpen

Naast het afvangen van excepties kan je deze ook zelf opwerpen met het keyword **raise**

Praktisch, stel je maakt een functie (dit leren we in een volgende les):

* Die de oppervlakte van een circel berekent
* Je wenst echter geen negatieve input

~~~python
import math

def oppervlakte(straal): 
  if straal < 0:
    raise Exception("Sorry, geen negatieve getallen")
  return 2 * straal * math.pi

oppervlakte(1)  # geeft als resultaat +- 6,283...
oppervlakte(-1) # geeft een error
~~~

De functie-aanroep op de laaste lijn zal het programma doen crashen en beëindigen.

~~~
6.283185307179586
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in oppervlakte
Exception: Sorry, geen negatieve getallen
~~~
