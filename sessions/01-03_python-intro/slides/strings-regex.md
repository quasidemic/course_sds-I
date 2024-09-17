## Tekst (strings) i Python

- Tekst-værdier i Python (og andre programmeringssprog) kaldes *strings*
- Strings er også en *class*
- Har en lang række indbyggede metoder

**Eksempler på string metoder**

| Metode | Forklaring | Objekt returneret |
| --- | --- | --- |
| `.lower()` | Lav om til små bogstaver (lower-case) | String |
| `.replace(old, new)` | Erstat tegn i tekst | String |
| `.startswith()` | Hvorvidt tekst starter med specifikke tegn | Boolean |
| `.split()` | Opdel tekst ved specifikt tegn | Liste |

---

## `in` operatoren i Python

- `in` kan bruges til at foretage simple tekstsøgninger
- `in` bruges i flere sammenhænge - er én ting en del af en anden ting?
- Returnerer altid boolean

<v-click>

**String eksempel**
```python
"hello" in "hello there" # er string til venstre en substring af string til højre?
```
</v-click>


<v-click>
```python
True
```
</v-click>


<v-click>

**Liste eksempel**


```python
"hello" in ["hello there", "hello world"] # er værdien til venstre en af værdierne i listen?
```
</v-click>

<v-click>
```python
False
```
</v-click>

---

## `in` operatoren i Python

**Dictionary eksempel**

```python
"hello" in {"hello": "there", "goodbye": "you"} # er værdien til venstre en key i dictionary?
```


<v-click>
```python
True
```
</v-click>

<v-click>
```python
"you" in {"hello": "there", "goodbye": "you"} # er værdien til venstre en key i dictionary?
```
</v-click>

<v-click>
```python
False
```
</v-click>

---

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

---
layout: center
---

# String metoder i Python (live coding)

---
layout: center
---

# Introduktion til regular expressions

https://www.regexpal.com/

```
"""
Der var tre drenge, der skulle ud i skoven. Den ene hed Jakob; de to andre hed Finn. 
så blev den ene Finn væk, så Jakob sagde til den anden Finn: "Finn find, Finn".
Finn kiggede mærkelig på Jakob og sagde: 'Jakob Jakob Jakob'.
"""
```

---

## Hvad er regular expressions?

- Samling af tegn der definerer mønster til tekstsøgning
- Er ikke specifikt til Python - implementeret i de fleste programmeringssprog
- Bruges til specifikke søgninger af ord, tekststykker og tekster

**Hvorfor bruge regular expressions?**
- Meget effektiv måde at lave søgninger og filtreringer på
- Mønstre kan lave utroligt specifikke og sofistikerede
- Effektiv til at lave filtreringer af tekststykker (uanset antal)

---

## Eksempel på regular expression

`^[KT]\w{5,8}\s[\d|\w]+`

*Oversat*: Find tekststykker, der starter med ord på 6-9 karakterer, som starter med enten stort K eller stort T, efterfulgt af et mellemrum, efterfulgt af et eller flere tal eller bogstaver.

<v-click>

*Eksempel*: Torvet 5e
</v-click>

---

## Regular expressions: Match flere tegn

|Forklaring|Tegn|Eksempel mønster|Matcher|
|--|--|--|--|
|Match flere tegn|`[]`|`[jJ]akob`|jakob, Jakob|
|Match flere tegn|`[]`|`[12345]`|Tallene 1-5|
|Range af tegn|`[x-y]`|`[A-Z]`|Et stort bogstav|
|Range af tegn|`[x-y]`|`[0-9]`|Et enkeltciffer|
|Negation|`[^x]`|`[^S]`|Ikke et stort S|
|Match flere tegnsamlinger (fx ord)|`\|`|`Jakob\|Finn`|Jakob eller Finn|

---

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

---

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

---

## Regular expressions: Look ahead / look behind

|Forklaring|Tegn|Eksempel mønster|Matcher|
|--|--|--|--|
|Mønster skal komme efter|`(?=)`|`\w+(?= kig)`|**Finn** kiggede mærkelig på Jakob|
|Mønster skal komme før|`(?<=)`|`(?<=på )\w+`|Finn kiggede mærkelig på **Jakob**|

---

## Escaping

- *Escaping* tillader, at man kan danne regular expression, der matcher tegnsætning som ".", "?" og andre tegn brugt i regular expression

- Man *escaper* et tegn (dvs. omgår dens betydning i regular expression) ved brug af `\`

**Eksempel**

|Mønster|Matcher|
|--|--|
|`kat?`|har du en **ka**t?, har du en **kat**?|
|`kat\?`|har du en **kat?**|

---

## Grupper

- Regular expressions kan opdeles i "undermønstre" (mønstre i mønstre) vha. grupper
- En regular expression *gruppe* angives med `()`

**Eksempel:**

`^[A-Z]\w+ (\w+)`

- Hele mønstret matcher tekst, der starter med et ord med stort forbogstav efterfulgt af et andet ord
- Gruppen (gruppe 1) matcher det andet ord

---

## Regular expressions i Python

- Brug pakken `re` (del af standardbibliotek)

*Definér mønster*: `re.compile()` (danner et  regex objekt `re.pattern`)

*Find match i start af tekst*: `re.match()`

*Find match et eller andet sted i tekst*: `re.search()` (altid det første match)

*Find all matches i en tekst*: `re.findall()` (returnerer altid en liste)

---

## Regular expressions i Python


```python
import re

text = "Jakob siger: 'Hej med dig, Finn'"

regex = re.compile("[A-Z]\w+")

regex.search(text) # matcher regex med tekst?
```

<v-click>
```python
<re.Match object; span=(0, 5), match='Jakob'>
```
</v-click>

<v-click>
```python
regex.findall(text) # hvilke tekststykker matcher?
```
</v-click>

<v-click>
```python
['Jakob', 'Hej', 'Finn']
```
</v-click>

---

## Regular expressions i Python

<v-click>
```python
text = "Jakob siger: 'Hej med dig, Finn'"

regex = re.compile("[A-Z]\w+ (\w+)")
```
</v-click>

<v-click>
```python
regex.search(text).group(1) # hvad matcher mønstret i gruppe 1?
```
</v-click>

<v-click>
```python
'siger'
```
</v-click>

<v-click>
```python
regex.findall(text) # hvilke tekststykker matcher mønstret i gruppe 1?
```
</v-click>

<v-click>
```python
['siger', 'med']
```
</v-click>

---

## Regular expressions i pandas

- Flere metoder i pandas understøtter regular expression (fx `.replace()`, `.str.replace()`, `.str.contains()`)
- Regular expressions kan også bruges til at udlede text fra én kolonne til en anden (med `.str.extract()`)
    - *Bemærk*: Udledning baseret på grupper i regular expression

<v-click>
```python
s = pd.Series(["cat", "dog", "house"])
s.str.contains("^\w{3}$", regex = True)
```
</v-click>

<v-click>

```python

    0     True
    1     True
    2    False
    dtype: bool
```
</v-click>

---

## Regular expressions i pandas

```python
s = pd.Series(["James Holden", "Bobbie Draper"])
s.str.extract("(^[A-Z]\w+)(?= )")
```

<v-click>

```python

    0     James
    1     Bobbie
    dtype: object
```

</v-click>

---
layout: center
---

# Regular expressions i Python (live-coding)

---

# ØVELSE: Regular expression i Python

Filen "soaf_characters.txt" i datamappen indeholder en liste over alle karakterer fra bogserien "A Song of Ice and Fire".

Find ud af hvor mange karakterer i bogserien, der har et efternavn, der starter med "T".

**Tips:**

- Hver karakter er adskilt af et linjeskift i filen. Tekstfilen kan laves om til en liste ved at splitte filen ved linjeskift: `.split('\n')`

---
layout: center
---

# Arbejd med længere tekster i Python (live-coding)

---

## Opsummering

- *Strings* i Python er en class, som har en række indbyggede metoder
- *Regular expressions* (`re` modulet) kan bruges til at lave søgninger på tekstmønstre frem for blot ord
- Regular expressions har mange anvendelser (søgning, filtrering, oprydning osv.)
