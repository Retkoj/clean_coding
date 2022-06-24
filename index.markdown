---
layout: home
list_title: Codeerconventies per programmeertaal
---

# Wat zijn codeer conventies?
Codeer conventies zijn afspraken en regels over het schrijven van code. Denk hierbij aan 
stijlafspraken, zoals de comments die je toevoegt, indentatie en de benaming van variabelen, maar ook aan het 
herbruikbaar maken en testen van code.  

Voor veel programmeertalen bestaan er codeerconventie standaarden, zoals [pep8](https://peps.python.org/pep-0008/) 
voor Python, [Tidyverse](https://style.tidyverse.org/) voor R, en de 
[SQL Style Guide](https://www.sqlstyle.guide/) van Simon Holywell. Daarnaast zijn er al veel artikelen geschreven
over het gebruik van codeerconventies en zullen organisaties zelf ook afspraken hebben. 

Dit document biedt een overzicht van codeer stijlconventies en andere best practices voor de meest gebruikte programmeertalen 
in Data Science: Python, R, en SQL. Hierbij wordt gebruik gemaakt van materiaal dat openbaar beschikbaar is – zoals 
bovengenoemde styleguides – en van praktijkervaringen binnen de overheid. 
Organisaties kunnen dit document gebruiken als beginpunt of leidraad voor hun eigen afspraken over codeerstandaarden.


# Waarom codeer conventies?

Codeer stijlconventies verbeteren de leesbaarheid van code en maken het daarmee makkelijker om:  
- peer review uit te voeren  
- code te begrijpen (zowel nieuwe code als eigen code die een tijd terug is geschreven)  
- code over te dragen aan een collega
- code te onderhouden of uit te breiden


Vergelijk onderstaande 2 stukken code maar eens. Deze 2 blokken hebben dezelfde functionaliteit, maar het tweede
blok is veel makkelijker te lezen.

{% highlight python %}
def func(n):
    a,b,i=0,1,0
    while i<n:
        print(a)
        c=a+b
        a,b=b,c
        i+=1
{% endhighlight %}


{% highlight python %}
def print_fibonacci_sequence(n_terms: int):
    """
    Print de eerst [n_terms] getallen van de Fibonacci serie naar de terminal.

    :param n_terms: Het gewenste aantal getallen dat geprint moet worden
    """
    current_number = 0
    next_number = 1
    count = 0
    while count < n_terms:
        print(current_number)
        next_sum = current_number + next_number
        current_number = next_number
        next_number = next_sum
        count += 1
{% endhighlight %}
