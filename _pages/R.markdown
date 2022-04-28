---
layout: page
title:  "R"
date:   2022-04-28
---
[tidyverse-styleguide]: https://style.tidyverse.org/
[styler-library]: https://styler.r-lib.org/
[lintr-library]: https://github.com/r-lib/lintr

# Inhoud  
- [Inleiding](#inleiding)  
- [Tidyverse](#tidyverse)  
- [Naamgeving](#naamgeving)  
- [Spaties, indentatie en witregels](#spaties-indentatie-en-witregels)  
- [Docstrings en comments](#docstrings-en-comments)  
- [Aangeraden uitzonderingen](#aangeraden-uitzonderingen)
  - [Logische waarden](#logische-waarden)  
  - [Expliciete functie output](#expliciete-functie-output)
- [Geautomatiseerd formatteren en controleren](#geautomatiseerd-formatteren-en-controleren)
  - [Styler](#styler)  
  - [Lintr](#lintr)   
- [Environments met renv](#environments-met-renv)

# Inleiding  

Deze pagina neemt als basis de Tidyverse styleguide voor R en zal de meest gebruikte practices, zoals naamgeving, 
en een aantal mogelijke uitzonderingen langsgaan. Voor Tydiverse, maar ook voor custom styleguides, zijn automatische
checks mogelijk, bijvoorbeeld d.m.v. [Styler][styler-library] en [Lintr][lintr-library]. Het is aan te raden dergelijke 
packages te gebruiken, zowel lokaal als in een Git pipeline.


# Tidyverse

De meest gebruikte styleguide voor R is de Tydiverse style guide 
([klik hier voor de volledige guide][tidyverse-styleguide]{:target="\_blank"}). 

Zoals de ontwikkelaars van Tidyverse zelf al aangeven, is Tidyverse niet de absolute waarheid of een verplichting 
waaraan elke programmeur moet voldoen:  
> All style guides are fundamentally opinionated. Some decisions genuinely do make code easier to use 
> (especially matching indenting to programming structure), but many decisions are arbitrary. 
> The most important thing about a style guide is that it provides consistency, making code easier to write because you 
> need to make fewer decisions.

De styleguide biedt een basis voor afspraken binnen het team of de organisatie over het schrijven van gestructureerde, 
leesbare en overdraagbare code.

# Naamgeving  

Voor de naamgeving van variabelen, functies, bestanden etc. kunnen de volgende richtlijnen worden aangehouden
- Gebruik snake case (dit houdt in dat variabelenamen lowercase zijn en dat woorden gescheiden zijn d.m.v. een underscore ( `_` ) )

{% highlight r %}
# Goed
my_variable <- 1

# Fout
myVariable <- 1
MyVariable <- 1
myvariable <- 1
{% endhighlight %}  
 
- Vermijd 1 letterige variabelenamen
{% highlight r %}
# Goed
employee <- "Jane"

# Fout
e <- "Jane"
{% endhighlight %}  
- Verkies een langere, beschrijvende naam boven een korte, onduidelijke naam. Vermijd dan ook onnodige
of ambigue afkortingen.
{% highlight r %}
# Goed
employee_number <- 123

# Fout
emp_n <- 123
{% endhighlight %}    

- Wees consistent in het werkwoord dat voor CRUD (create, read, update, delete) operaties gebruikt wordt, 
  e.g. ‘create’, ‘get’, ‘update’, en ‘remove’.
{% highlight r %}
# Goed
get_employee_by_id <- function(employee_id) {...}
get_department_by_id <- function(department_id) {...}
get_city_by_id <- function(city_id) {...}

# Fout
get_employee_by_id <- function(employee_id) {...}
retrieve_department_by_id <- function(department_id) {...}
extract_city_by_id <- function(city_id) {...}
{% endhighlight %}    

- Gebruik geen werkwoorden in variabelenamen, maar wel in functienamen
{% highlight r %}
# Goed
get_employee_by_id <- function(employee_id) {...}
employee <- get_employee_by_id(123)

# Fout
employee_by_id <- function(employee_id) {...}
employee <- function() {...}
get_employee <- "Jane"
{% endhighlight %}   

- Gebruik Engelse variabele- en functienamen. 
- Docstrings en comments kunnen Nederlands of Engels zijn, afhankelijk van de internationaliteit van de organisatie,
  maar wees daarin wel consistent.

# Spaties, indentatie en witregels

Voor spaties, indentaties en witregels kunnen de volgende richtlijnen worden aangehouden:  
- Gebruik 2 spaties om te indenteren
- Zet de openende curly bracket (`{`) op de regel met de functie
- Zet de sluitende curly bracket (`}`) op een eigen regel
{% highlight r %}
# Goed
get_sum <- function(left_hand_number, right_hand_number) {
  return(a + b)
}

# Fout
get_sum <- function(left_hand_number, right_hand_number) { return(a + b) }
get_sum <- function(left_hand_number, right_hand_number) 
{ return(a + b) }

get_sum <- function(left_hand_number, right_hand_number) { 
return(a + b) 
}
{% endhighlight %}  


# Docstrings en comments

# Aangeraden uitzonderingen

#### Logische waarden

Gebruik niet `T` en `F` voor logische waarden, maar expliciet `TRUE` en `FALSE`. `T` en `F` zijn variabelen die 
standaard zijn ingesteld op de waarden `TRUE` en `FALSE`, maar het zijn geen gereserveerde woorden en kunnen daarom 
door de gebruiker worden overschreven. 

#### Expliciete functie output

Een functie moet altijd eindigen met een expliciet `return()` statement of met `invisible()`. De functie
`invisible()` gebruik je wanneer de functie niets moet teruggeven. Wanneer je de functie `invisible()` niet
gebruikt dan zal het resultaat van het laatste statement terug worden gegeven, en dat kan tot onverwachte resultaten of
fouten leiden.

# Geautomatiseerd formatteren en controleren

[Styler][styler-library] en [Lintr][lintr-library] zijn twee packages die het makkelijker maken om aan de Tidyverse 
styleguide te voldoen. Styler biedt zowel een plugin voor RStudio als een command line interface waarmee je je 
scripts kan formatteren in lijn met de Tidyverse styleguide. Lintr biedt een check op je code om te zien of
deze voldoet aan de styleguide, of er syntaxerrors zijn, en of er sematische problemen zijn.

#### Styler

Styler kan geïnstalleerd worden met het volgende commando:  
{% highlight r %}
install.packages("styler")
{% endhighlight %}  

Na het installeren kan je Styler vinden in de addin dropdown in RStudio. Zie hieronder een voorbeeld van code 
voor en na het gebruik van Styler:  
![Styler add-in before](../images/styler_addin_unformatted_code.PNG)  

![Styler add-in after](../images/styler_addin_formatted_code.PNG)

#### Lintr
Lintr kan geïnstalleerd worden met het volgende commando:  
{% highlight r %}
install.packages("lintr")
{% endhighlight %}  

Na het installeren kan je Lintr vinden in de addin dropdown in RStudio. Zie hieronder een voorbeeld van output
gegenereerd door Lintr:  

![Lintr markers](../images/lintr_addin_unformatted_code.PNG) 

Ook kan je Lintr in de console gebruiken om bijvoorbeeld de hele directory te controleren:  
{% highlight r %}
lintr::lint_dir()
{% endhighlight %} 

# Environments met renv
