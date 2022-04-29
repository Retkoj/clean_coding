---
layout: page
title:  "Python"
date:   2022-04-08 13:59:34 +0200
categories: jekyll update
---
[pep8-documentation]: https://peps.python.org/pep-0008/
[pep8-white-space-exceptions]: https://peps.python.org/pep-0008/#whitespace-in-expressions-and-statements

# Inhoud
- [Inleiding](#inleiding) 
- [Pep8](#pep8)
- [Naamgeving](#naamgeving)
- [Spaties, indentatie en witregels](#spaties-indentatie-en-witregels)
- [Imports](#imports)  
- [Docstrings en comments](#docstrings-en-comments) 
- [Reproduceerbaarheid](#reproduceerbaarheid)
   - [Requirements](#requirements)
   - [Virtual env](#virtual-env)
   - [Conda environment](#conda-environment)

# Inleiding

Deze pagina neemt als basis de <ins>[Pep8 styleguide voor Python][pep8-documentation]{:target="\_blank"}</ins> en zal de meest gebruikte practices, 
zoals naamgeving, en een aantal mogelijke uitzonderingen langsgaan. Veel IDE's, zoals PyCharm of Visual Studio, hebben
de mogelijkheid om code automatisch te formatteren of the controleren op format fouten. Het is aan te raden dergelijke 
checks te gebruiken, zowel lokaal als in een Git pipeline.

# Pep8
De meest gebruikte styleguide voor Python is de Pep8 style guide 
(<ins>[klik hier voor de volledige guide][pep8-documentation]{:target="\_blank"}</ins>). 

Zoals het geval is met elke styleguide, is Pep8 niet de absolute waarheid of een verplichting 
waaraan elke programmeur moet voldoen. Ook zijn niet alle delen van de guide even relevant voor alle teams.
De styleguide biedt een basis voor afspraken binnen het team of de organisatie over het schrijven van gestructureerde, 
leesbare en overdraagbare code.

# Naamgeving

Voor de naamgeving van variabelen, functies, bestanden etc. kunnen de volgende richtlijnen aangehouden worden:  
- Gebruik snake case (dit houdt in dat variabelenamen lowercase zijn en dat woorden gescheiden zijn d.m.v. een underscore ( `_` ) )

{% highlight python %}
# Goed
my_variable = 1

# Fout
myVariable = 1
MyVariable = 1
myvariable = 1
{% endhighlight %}  
 
- Vermijd 1 letterige variabelenamen
{% highlight python %}
# Goed
employee = "Jane"

# Fout
e = "Jane"
{% endhighlight %}  
- Verkies een langere, beschrijvende naam boven een korte, onduidelijke naam. Vermijd dan ook onnodige
of ambigue afkortingen.
{% highlight python %}
# Goed
employee_number = 123

# Fout
emp_n = 123
{% endhighlight %}    

- Wees consistent in het werkwoord dat voor CRUD (create, read, update, delete) operaties gebruikt wordt, 
  e.g. ‘create’, ‘get’, ‘update’, en ‘remove’.
{% highlight python %}
# Goed
def get_employee_by_id(employee_id):
   pass
def get_department_by_id(department_id):
   pass
def get_city_by_id(city_id):
   pass

# Fout
def get_employee_by_id(employee_id):
   pass
def retrieve_department_by_id(department_id):
   pass
def extract_city_by_id(city_id):
   pass
{% endhighlight %}    

- Gebruik geen werkwoorden in variabelenamen, maar wel in functienamen
{% highlight python %}
# Goed
def get_employee_by_id(employee_id):
   pass
employee = get_employee_by_id(123)

# Fout
def employee_by_id(employee_id):
   pass
def employee(employee_id):
   pass
get_employee = "Jane"
{% endhighlight %}   

- Gebruik Engelse variabele- en functienamen. 
- Docstrings en comments kunnen Nederlands of Engels zijn, afhankelijk van de internationaliteit van de organisatie,
  maar wees daarin wel consistent.

# Spaties, indentatie en witregels

Voor spaties, indentaties en witregels kunnen de volgende richtlijnen aangehouden worden:
- Gebruik bij indentaties 4 spaties i.p.v. een tab. Bij veel IDE's, zoals PyCharm, is dit in te stellen als standaard:  
![PyCharm Python indentation setting](../images/pycharm_indent_setting_python.PNG)

- Zet spaties om operators (e.g. `+`, `-`, `+=`, `*`). Uitzonderingen hier op zijn bijvoorbeeld de `**` operator en de ruimte direct na openende 
  haakjes(e.g. `(`, `{`) of direct voor sluitende haakjes (e.g. `)`, `}`). Voor een vollediger overzicht van uitzonderingen,
  zie de <ins>[Pep8 documentatie][pep8-white-space-exceptions]{:target="\_blank"}</ins> Bij veel IDE's, zoals PyCharm, is dit in te stellen als standaard 
  (Te vinden onder het tabblad 'Spaces' in de PyCharm screenshot hierboven)
{% highlight python %}
# Goed
answer = 40 + 2
hypotenuse = sqrt(opposite_side**2 + adjacent_side**2)

# Fout
answer=40+2
hypotenuse = sqrt ( opposite_side ** 2 + adjacent_side ** 2 )
{% endhighlight %}   

- Gebruik 2 witregels na functies en classes
- Gebruik 1 witregel tussen functies binnen classes
- Gebruik witregels binnen functies met mate en alleen om logische blokken aan te geven


# Imports

Om de gebruikte imports overzichtelijk te houden kunnen de volgende regels gebruikt worden:

- Cluster imports d.m.v. witregels op basis van type import. 
- Hou bij de clustering van imports de volgende volgorde aan:
    - Standaard library imports (e.g. `os`)
    - Related third party imports (e.g. `pandas`)
    - Local application/library specific imports (e.g. `from my_local_script import local_function`)
- Zet elke import op een eigen regel   
- Vermijd het gebruik van wildcards (`*`), omdat dit onduidelijk maakt welke functies of variabelen geïmporteerd worden

{% highlight python %}
# Goed
import os
import sys
from subprocess import Popen, PIPE

import numpy as np
import pandas as pd

from my_local_script import my_function 

# Fout
import numpy as np
from subprocess import *
from my_local_script import my_function
import pandas as pd
import os, sys
{% endhighlight %}


# Docstrings en comments
Docstrings, of documentation strings, zijn strings die het doel en gebruik van een functie, class of module 
verduidelijken. 

- Het is good practice om alle functies, classes en modules van documentatie te voorzien.   

- Voor grote of complexe functies kan de volgende opzet gebruikt worden (De formatting kan afwijken per team):  
{% highlight python %}
def some_function(some_parameter):
    """
    Beschrijving van functie en gebruik

    :param some_parameter: Integer, Korte beschrijving van parameter
    :return: Beschrijving van de output van de functie
    """
    pass
{% endhighlight %}

- Wanneer het doel en gebruik van de functie overduidelijk is, kan er ook voor een one-liner gekozen worden:   
{% highlight python %}
def calculate_hypotenuse(adjacent_side, opposite_side) -> float:
    """Berekent de hypotenusa van een driehoek."""
    return sqrt(opposite_side**2 + adjacent_side**2)
{% endhighlight %}

- Maak over het gebruik van comments in je code goede afspraken binnen je team: sommige teams geven de voorkeur aan
  veel comments, terwijl anderen juist helemaal geen comments willen gebruiken. 
- Vaak is het beter om de code leesbaarder te maken dan veel comments toe te voegen:  
{% highlight python %}
employee = "Jane"
add_employee_to_database(employee)
  
# Versus:

e = "Jane"
func(e)  # Voeg Jane toe aan de database
{% endhighlight %}

<b>houdt de comments en docstrings goed bij: wanneer de code geüpdate wordt, moeten ook alle comments en docstrings 
geüpdate worden</b>

# Reproduceerbaarheid

#### Requirements

#### Virtual env

#### Conda environment

{% highlight python %}
def print_hi(name):
   print(f"Hi, {name}")

print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

