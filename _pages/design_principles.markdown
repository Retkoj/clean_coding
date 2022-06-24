---
layout: page
title:  "Design Principles"
date:   2022-04-08 13:59:34 +0200
categories: jekyll update
---

## KISS

Keep It Simple, Stupid (of "Keep it simple, silly", "keep it short and simple", "keep it short and sweet", 
"keep it simple and straightforward", "keep it small and simple", "keep it simple, soldier", "keep it simple, sailor", 
"keep it sweet and simple".)  

In essentie: Hou de code simpel en leesbaar.

{% highlight python %}
# Leesbaar:
def faculty(number: int) -> int:
    if number <= 1:
        return 1
    else:
        return number * faculty(number - 1)

# Complex/Minder leesbaar:
f = lambda x: 1 if x <= 1 else x * f(x - 1)

{% endhighlight %}
(Voorbeeld overgenomen van: https://code-specialist.com/code-principles/kiss)
## DRY

Het 'Don't Repeat Yourself'(DRY)-Principe stelt -zoals de naam suggereert- dat je jezelf niet moet herhalen.
Wanneer je merkt dat je hetzelfde stukje code opnieuw aan het schrijven bent, dan heb je waarschijnlijk genoeg materiaal
voor een (generiekere) functie.


Zie de twee stukken code hieronder voor een voorbeeld:  
{% highlight python %}

# Herhalende code:
print("1: a")
print("2: b")
print("3: c")
print("4: d")
print("5: e")
...

# DRY:
from string import ascii_lowercase as alphabet

for index, letter in enumerate(alphabet):
    print(f"{index + 1}: {letter}")

{% endhighlight %}


## Magic Numbers

{% highlight python %}
# Met magic numbers:
def total_price(costs: float):
    total_costs = costs + (costs * 0.21)
    total_costs = costs + 4.95
    return total_costs

# Verduidelijkt:
SHIPPING_FEE = 4.95
TAX = 0.21

def total_price(costs: float):
    total_costs = costs + (costs * TAX)
    total_costs = costs + SHIPPING_FEE
    return total_costs

{% endhighlight %}

# Gebruik bij gegroepeerde waardes bijv. een enum of dictionary (Python) of list (R):
{% highlight python %}
from enum import Enum

class ShippingFees(Enum):
    LETTER = 1.50
    SMALL_PACKAGE = 4.95
    LARGE_PACKAGE = 9.95

TAX = 0.21

def total_price(costs: float, shipping_fee_type: ShippingFees):
    total_costs = costs + (costs * TAX)
    total_costs = costs + shipping_fee_type.value
    return total_costs

total_price(3, ShippingFees.SMALL_PACKAGE)

{% endhighlight %}
{% highlight r %}
SHIPPING_FEES <- list(LETTER = 1.50, 
                      SMALL_PACKAGE = 4.95, 
                      LARGE_PACKAGE = 9.95)

TAX <- 0.21

total_price <- function(costs, shipping_fee) {
    total_costs <- costs + (costs * TAX)
    total_costs <- costs + shipping_fee
    return(total_costs)
}

total_price(3, SHIPPING_FEES$SMALL_PACKAGE)

{% endhighlight %}

## YAGNI

You ain't gonna need it!  
Codeer alleen functionaliteit die je nu nodig hebt. Hou niet rekening met elk mogelijke
feature die ooit nog handig zou kunnen zijn.  
Door alleen te coderen wat er nu nodig is:  
- Blijft de code compacter en efficiënter: Er is geen/minder ongebruikte code
- Hou je meer tijd over voor de code die daadwerkelijk nodig is
- Loop je niet tegen onnodig veel werk aan bij refactoren

{% highlight python %}
from pathlib import Path

# 'Het is nu een csv, maar dat kan ooit veranderen'
def get_users(file_path: str):
    users = None
    extension = Path(file_path).suffix
    if extension == '.csv':
        users = pd.read_csv(file_path)
    elif extension == '.json':
        users = pd.read_json(file_path)
    elif extension == '.pdf':
        ...
    
    return users

# Als er nu alleen een csv bestand gebruikt wordt, schrijf dan alleen die code
def get_users(file_path: str):
    return pd.read_csv(file_path)

{% endhighlight %}
## Single Responsibility Principle

{% highlight python %}
import pandas as pd

# Meerdere functionaliteiten in één functie
def get_user_record(user_id: int, users_file_path: str, new_role: str):
    users = pd.read_csv(users_file_path)
    users.loc[users['user_id'] == user_id, 'role'] = new_role
    user = all_users[users['user_id'] == user_id]
    users.to_csv(users_file_path)
    return user

# Functionaliteiten uitgesplitst:
def get_all_users(users_file_path: str):
    return pd.read_csv(users_file_path)


def set_new_role(users: pd.DataFrame, user_id: int, new_role: str):
    users.loc[users['user_id'] == user_id, 'role'] = new_role
    return users


def save_users_to_csv(users: pd.DataFrame, users_file_path: str):
    users.to_csv(users_file_path)


def get_user_record(users: pd.DataFrame, user_id: int)
    return all_users[users['user_id'] == user_id]

{% endhighlight %}