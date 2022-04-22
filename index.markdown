---
layout: home
list_title: Codeerconventies per programmeertaal
---

# Wat zijn codeer conventies?
Codeer conventies zijn afspraken die gemaakt worden bij het schrijven van code. Denk hierbij bijvoorbeeld aan 
stijlafspraken, zoals de 
comments die je toevoegt, indentatie en de benaming van variabelen, maar ook aan het herbruikbaar maken en testen van code.

# Waarom codeer stijlconventies?

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
