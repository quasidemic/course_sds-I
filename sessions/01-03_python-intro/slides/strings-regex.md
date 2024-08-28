```python
# prep

import pandas as pd
import re
from datetime import datetime

text = """Der var tre drenge, der skulle ud i skoven. Den ene hed Jakob; de to andre hed Finn. 
så blev den ene Finn væk, så Jakob sagde til den anden Finn: "Finn find, Finn".
Finn kiggede mærkelig på Jakob og sagde: 'Jakob Jakob Jakob'."""
```

# Introduktion til Python II - Tid og tekst i Python

## Program

- Opfølgning fra sidste undervisningsgang
- Tekst (strings) i Python
- Introduktion til regular expressions
- Brug af strings metoder og regular expressions i pandas data frames
- Datoer og tid i Python
- Datoer og tid i pandas data frames

# Opfølgning fra sidste undervisningsgang

## Strings i Python

- Strings er også en *class*
- Har en lang række indbyggede metoder

**Eksempler på string metoder**

| Metode | Forklaring | Objekt returneret |
| --- | --- | --- |
| `.lower()` | Lav om til små bogstaver (lower-case) | String |
| `.replace(old, new)` | Erstat tegn i tekst | String |
| `.startswith()` | Hvorvidt tekst starter med specifikke tegn | Boolean |
| `.split()` | Opdel tekst ved specifikt tegn | Liste |

<table>
<thead>
<tr><th>Metode</th><th>Forklaring</th><th>Objekt returneret</th></tr></thead>
<tbody><tr><td><code>.lower()</code></td><td>Lav om til små bogstaver (lower-case)</td><td>String</td></tr><tr><td><code>.replace(old, new)</code></td><td>Erstat tegn i tekst</td><td>String</td></tr><tr><td><code>.startswith()</code></td><td>Hvorvidt tekst starter med specifikke tegn</td><td>Boolean</td></tr><tr><td><code>.split()</code></td><td>Opdel tekst ved specifikt tegn</td><td>Liste</td></tr></tbody>
</table>

## `in` operatoren i Python

- `in` bruges i flere sammenhænge - er én ting en del af en anden ting?
- Returnerer altid boolean

**String eksempel**


```python
"hello" in "hello there" # er string til vesntre en substring af string til højre?
```




    True



**Liste eksempel**


```python
"hello" in ["hello there", "hello world"] # er værdien til venstre en af værdierne i listen?
```




    False



**Dictionary eksempel**


```python
"hello" in {"hello": "there", "goodbye": "there"} # er værdien til venstre en key i dictionary?
```




    True




```python
"you" in {"hello": "there", "goodbye": "you"} # er værdien til venstre en key i dictionary?
```




    False



## String metoder i pandas

- De fleste string metoder findes i pandas også
- Tilgås under `.str`

**Eksempler (base python - pandas)**

|Base|Pandas|
|--|--|
|`.lower()`|`.str.lower()`|
|`.replace()`|`.str.replace()`|
|`.startswith()`|`.str.startswith()`|
|`in`|`.str.contains()`|

<table>
<thead>
<tr><th>Base</th><th>Pandas</th></tr></thead>
<tbody><tr><td><code>.lower()</code></td><td><code>.str.lower()</code></td></tr><tr><td><code>.replace()</code></td><td><code>.str.replace()</code></td></tr><tr><td><code>.startswith()</code></td><td><code>.str.startswith()</code></td></tr><tr><td><code>in</code></td><td><code>.str.contains()</code></td></tr></tbody>
</table>

# String metoder i Python (live coding)

# Introduktion til regular expressions

https://www.regexpal.com/

## Hvad er regular expressions?

- Samling af tegn der definerer mønster til tekstsøgning
- Er ikke specifikt til Python - implementeret i de fleste programmeringssprog
- Bruges til specifikke søgninger af ord, tekststykker og tekster

**Hvorfor bruge regular expressions?**
- Meget effektiv måde at lave søgninger og filtreringer på
- Mønstre kan lave utroligt specifikke og sofistikerede
- Effektiv til at lave filtreringer af tekststykker (uanset antal)

## Eksempel på regular expression

`^[KT]\w{5,8}\s[\d|\w]+`

*Oversat*: Find tekststykker, der starter med ord på 6-9 karakterer, som starter med enten stort K eller stort T, efterfulgt af et mellemrum, efterfulgt af et eller flere tal eller bogstaver.

*Eksempelvis*: Torvet 5e

## Regular expressions: Match flere tegn

|Forklaring|Tegn|Eksempel mønster|Matcher|
|--|--|--|--|
|Match flere tegn|`[]`|`[jJ]akob`|jakob, Jakob|
|Match flere tegn|`[]`|`[12345]`|Tallene 1-5|
|Range af tegn|`[x-y]`|`[A-Z]`|Et stort bogstav|
|Range af tegn|`[x-y]`|`[0-9]`|Et enkeltciffer|
|Negation|`[^x]`|`[^S]`|Ikke et stort S|
|Match flere tegnsamlinger (fx ord)|`\|`|`Jakob\|Finn`|Jakob eller Finn|

<table>
<thead>
<tr><th>Forklaring</th><th>Tegn</th><th>Eksempel mønster</th><th>Matcher</th></tr></thead>
<tbody><tr><td>Match flere tegn</td><td><code>[]</code></td><td><code>[jJ]akob</code></td><td>jakob, Jakob</td></tr><tr><td>Match flere tegn</td><td><code>[]</code></td><td><code>[12345]</code></td><td>Tallene 1-5</td></tr><tr><td>Range af tegn</td><td><code>[x-y]</code></td><td><code>[A-Z]</code></td><td>Et stort bogstav</td></tr><tr><td>Range af tegn</td><td><code>[x-y]</code></td><td><code>[0-9]</code></td><td>Et enkeltciffer</td></tr><tr><td>Negation</td><td><code>[^x]</code></td><td><code>[^S]</code></td><td>Ikke et stort S</td></tr><tr><td>Match flere tegnsamlinger (fx ord)</td><td><code>\|</code></td><td><code>Jakob\|Finn</code></td><td>Jakob eller Finn</td></tr></tbody>
</table>

## Regular expressions: Wildcard-søgninger

|Forklaring|Tegn|Eksempel mønster|Matcher|
|--|--|--|--|
|Valgfri karakter (match 1 eller 0 gange)|`?`|`Kath?rine`|Kathrine, Katrine|
|Match 0 eller flere gange|`*`|`haa*!`|ha!, haa!, haaa!, haaaa!, ...|
|Match 1 eller flere gange|`+`|`haa+!`|haa!, haaa!, haaaa!, ...|
|Match hvilken som helst karakter|`.`|`.us`|mus, lus, hus, bus|
|Match start af string|`^`|`^F`|**F**inn kiggede mærkeligt|
|Match enden af string|`$`|`t$`|Finn kiggede mærkelig**t**|
|Gentag mønster|`{x,y}`|`Fin{1,2}`|**Fin**n kiggede mærkeligt, **Finn** kiggede mærkeligt|

<table>
<thead>
<tr><th>Forklaring</th><th>Tegn</th><th>Eksempel mønster</th><th>Matcher</th></tr></thead>
<tbody><tr><td>Valgfri karakter (match 1 eller 0 gange)</td><td><code>?</code></td><td><code>Kath?rine</code></td><td>Kathrine, Katrine</td></tr><tr><td>Match 0 eller flere gange</td><td><code>*</code></td><td><code>haa*!</code></td><td>ha!, haa!, haaa!, haaaa!, ...</td></tr><tr><td>Match 1 eller flere gange</td><td><code>+</code></td><td><code>haa+!</code></td><td>haa!, haaa!, haaaa!, ...</td></tr><tr><td>Match hvilken som helst karakter</td><td><code>.</code></td><td><code>.us</code></td><td>mus, lus, hus, bus</td></tr><tr><td>Match start af string</td><td><code>^</code></td><td><code>^F</code></td><td><strong>F</strong>inn kiggede mærkeligt</td></tr><tr><td>Match enden af string</td><td><code>$</code></td><td><code>t$</code></td><td>Finn kiggede mærkelig<strong>t</strong></td></tr><tr><td>Gentag mønster</td><td><code>{x,y}</code></td><td><code>Fin{1,2}</code></td><td><strong>Fin</strong>n kiggede mærkeligt, <strong>Finn</strong> kiggede mærkeligt</td></tr></tbody>
</table>

## Regular expressions: Match typer af tegn

|Forklaring|Tegn|
|--|--|
|Match "word character"|`\w`|
|Match *ikke* "word character"|`\W`|
|Match et tal|`\d`|
|Match et "whitespace"|`\s`|
|Match *ikke* et "whitespace"|`\S`|
|Match et linjeskift|`\n`|
|Match et linjeskift|`\r`|
|Match en ordafgrænsning (tegnsætning, whitespace, linjeskift)|`\b`|

<table>
<thead>
<tr><th>Forklaring</th><th>Tegn</th></tr></thead>
<tbody><tr><td>Match &quot;word character&quot;</td><td><code>\w</code></td></tr><tr><td>Match <em>ikke</em> &quot;word character&quot;</td><td><code>\W</code></td></tr><tr><td>Match et tal</td><td><code>\d</code></td></tr><tr><td>Match et &quot;whitespace&quot;</td><td><code>\s</code></td></tr><tr><td>Match <em>ikke</em> et &quot;whitespace&quot;</td><td><code>\S</code></td></tr><tr><td>Match et linjeskift</td><td><code>\n</code></td></tr><tr><td>Match et linjeskift</td><td><code>\r</code></td></tr><tr><td>Match en ordafgrænsning (tegnsætning, whitespace, linjeskift)</td><td><code>\b</code></td></tr></tbody>
</table>

## Regular expressions: Look ahead / look behind

|Forklaring|Tegn|Eksempel mønster|Matcher|
|--|--|--|--|
|Mønster skal komme efter|`(?=)`|`\w+(?= kig)`|**Finn** kiggede mærkelig på Jakob|
|Mønster skal komme før|`(?<=)`|`(?<=på )\w+`|Finn kiggede mærkelig på **Jakob**|

<table>
<thead>
<tr><th>Forklaring</th><th>Tegn</th><th>Eksempel mønster</th><th>Matcher</th></tr></thead>
<tbody><tr><td>Mønster skal komme efter</td><td><code>(?=)</code></td><td><code>\w+(?= kig)</code></td><td><strong>Finn</strong> kiggede mærkelig på Jakob</td></tr><tr><td>Mønster skal komme før</td><td><code>(?&lt;=)</code></td><td><code>(?&lt;=på )\w+</code></td><td>Finn kiggede mærkelig på <strong>Jakob</strong></td></tr></tbody>
</table>

## Escaping

- *Esccaping* tillader, at man kan danne regular expression, der matcher tegnsætning som ".", "?" og andre tegn brugt i regular expression

- Man *escaper* et tegn (dvs. omgår dens betydning i regular expression) ved brug af `\`

**Eksempel**

|Mønster|Matcher|
|--|--|
|`kat?`|har du en **ka**t?, har du en **kat**?|
|`kat\?`|har du en **kat?**|

<table><thead><tr><th><span>Mønster</span></th><th><span>Matcher</span></th></tr></thead><tbody><tr><td><code>kat?</code></td><td><span>har du en </span><strong><span>ka</span></strong><span>t?, har du en </span><strong><span>kat</span></strong><span>?</span></td></tr><tr><td><code>kat\?</code></td><td><span>har du en </span><strong><span>kat?</span></strong></td></tr></tbody></table>

## Grupper

- Regular expressions kan opdeles i "undermønstre" (mønstre i mønstre) vha. grupper
- En regular expression *gruppe* angives med `()`

**Eksempel:**

`^[A-Z]\w+ (\w+)`

- Hele mønstret matcher tekst, der starter med et ord med stort forbogstav efterfulgt af et andet ord
- Gruppen (gruppe 1) matcher det andet ord

## Regular expressions i Python

- Brug pakken `re` (del af standardbibliotek)

*Definér mønster*: `re.compile()` (danner et  regex objekt `re.pattern`)

*Find match i start af tekst*: `re.match()`

*Find match et eller andet sted i tekst*: `re.search()` (altid det første match)

*Find all matches i en tekst*: `re.findall()` (returnerer altid en liste)

## Regular expressions i Python


```python
import re

text = "Jakob siger: 'Hej med dig, Finn'"

regex = re.compile("[A-Z]\w+")

regex.search(text) # matcher regex med tekst?
```




    <re.Match object; span=(0, 5), match='Jakob'>




```python
regex.findall(text) # hvilke tekststykker matcher?
```




    ['Jakob', 'Hej', 'Finn']



## Regular expressions i Python


```python
text = "Jakob siger: 'Hej med dig, Finn'"

regex = re.compile("[A-Z]\w+ (\w+)")

regex.search(text).group(1) # hvad matcher mønstret i gruppe 1?
```




    'siger'




```python
regex.findall(text) # hvilke tekststykker matcher mønstret i gruppe 1?
```




    ['siger', 'med']



## Regular expressions i pandas

- Flere metoder i pandas understøtter regular expression (fx `.replace()`, `.str.replace()`, `.str.contains()`)
- Regular expressions kan også bruges til at udlede text fra én kolonne til en anden (med `.str.extract()`)
    - *Bemærk*: Udledning baseret på grupper i regeular expression


```python
s = pd.Series(["cat", "dog", "house"])
s.str.contains("^\w{3}$", regex = True)
```




    0     True
    1     True
    2    False
    dtype: bool




```python
s = pd.Series(["James Holden", "Bobbie Draper"])
s.str.extract("(^[A-Z]\w+)(?= )")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>James</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bobbie</td>
    </tr>
  </tbody>
</table>
</div>



# Regular expressions i Python (live-coding)

# ØVELSE: Regular expression i Python

Filen "soaf_characters.txt" i datamappen indeholder en liste over alle karakterer fra bogserien "A Song of Ice and Fire".

Find ud af hvor mange karakterer i bogserien, der har et efternavn, der starter med "T".

**Tips:**
- Hver karakter er adskilt af et linjeskift i filen. Tekstfilen kan laves om til en liste ved at splitte filen ved linjeskift: `.split('\n')`
- Funktionen `set()` danner et sæt af unikke værdier i en liste


# Arbejd med længere tekster i Python (live-coding)

## Opsummering

- *Strings* i Python er en class, som har en række indbyggede metoder
- *Regular expressions* (`re` modulet) kan bruges til at lave søgninger på tekstmønstre frem for blot ord
- Regular expressions har mange anvendelser
