# Dataformater og datastrukturer

## Data -> Datasæt -> Datastruktur

![data-structure](../img/data_set_structure.png)

---

## Relationel datastruktur

- Data i tabeller
- Hver tabel har kun 2 dimensioner (rækker og kolonner)

![hierarch](../img/expanse_relational.png){width=20% lazy}

---

## Hierarkisk datastruktur

- Data i træ-lignende struktur
- Ikke bundet til 2 dimensioner (hver gren kan have så mange undergrene, som  der er behov for)

![hierarch](../img/expanse_hierarchical.png){width=70% lazy}

---

## Hyppige datafilformater: .csv

- csv: "Comma-separated values"
- Én række per observation
- Værdier adskilt med kommaer
- To-dimensionel datastruktur

<v-click>
```
name,ethnicity,vocation
James,earther,captain
Naomi,belter,technician
Alex,martian,pilot
Clarissa,earther,mechanic
```
</v-click>

---
layout: two-cols
---

## Hyppige datafilformater: .json

- Hierarkisk dataformat
- Værdier i nøgle-værdi par
- Flere "grene" kan tilføjes

::right::

```
{'Nemesis Games': {
    "Characters": {
        "James Holden": {
            "Occupation": "Captain", 
            "Ethnicity": "Earther", 
            "Ship": {
                "Name": "Rocinante",
                "Class": "Corvette",
                "Owner": "James Holden",
                "Crew-size": 6
            }
        },
        "Naomi Nagata": {
            "Occupation": "Technician", 
            "Ethnicity": "Belter",
            "Children": {
                "Filip Nagata": {
                    "Name": "Filip Nagata",
                    "Occupation": "Unknown"
                }
            }
        }
    }
}
```

---

## Datastruktur i Python: Liste af lister


```python
names = ["James", "Naomi", "Alex", "Clarissa"]
ethnicities = ["earther", "belter", "martian", "earter"]
vocation = ["captain", "technician", "pilot", "mechanic"]

data = [names, ethnicities, vocation]
```

<v-click>
```
# data
[['James', 'Naomi', 'Alex', 'Clarissa'],
 ['earther', 'belter', 'martian', 'earter'],
 ['captain', 'technician', 'pilot', 'mechanic']]
```
</v-click>

<v-click>
```python
[items[0] for items in data]
```
</v-click>

<v-click>
```
['James', 'earther', 'captain']
```
</v-click>

---

## Datastruktur i Python: Dictionary (JSON)


```python
data = {
    "James": {"ethnicity": "earther", "vocation": "captain"},
    "Naomi": {"ethnicity": "belter", "vocation": "technician"},
    "Alex": {"ethnicity": "martian", "vocation": "pilot"},
    "Clarissa": {"ethnicity": "earther", "vocation": "mechanic"},
}
```

```
# data
{'James': {'ethnicity': 'earther', 'vocation': 'captain'},
 'Naomi': {'ethnicity': 'belter', 'vocation': 'technician'},
 'Alex': {'ethnicity': 'martian', 'vocation': 'pilot'},
 'Clarissa': {'ethnicity': 'earther', 'vocation': 'mechanic'}}
```

<v-click>
```python
data["James"]
```
</v-click>

<v-click>
```
{'ethnicity': 'earther', 'vocation': 'captain'}
```
</v-click>

---

## Datastruktur i Python: Liste af dictionaries (JSON records)


```python
data = [
    {"name": "James", "ethnicity": "earther", "vocation": "captain"},
    {"name": "Naomi", "ethnicity": "belter", "vocation": "technician"},
    {"name": "Alex", "ethnicity": "martian", "vocation": "pilot"},
    {"name": "Clarissa", "ethnicity": "earther", "vocation": "mechanic"},
]
```

```
# data
[{'name': 'James', 'ethnicity': 'earther', 'vocation': 'captain'},
 {'name': 'Naomi', 'ethnicity': 'belter', 'vocation': 'technician'},
 {'name': 'Alex', 'ethnicity': 'martian', 'vocation': 'pilot'},
 {'name': 'Clarissa', 'ethnicity': 'earther', 'vocation': 'mechanic'}]
```

<v-click>
```python
data[0]
```
</v-click>

<v-click>
```
{'name': 'James', 'ethnicity': 'earther', 'vocation': 'captain'}
```
</v-click>

---

## Datastruktur i Python: (pandas) Data frame


```python
import pandas as pd

data = pd.DataFrame.from_records(data)
```

![hierarch](../img/expanse_relational.png){width=20% lazy}

<v-click>
```python
data.loc[0, :]
```
</v-click>

<v-click>

```python
    name           James
    ethnicity    earther
    vocation     captain
    Name: 0, dtype: object
```
</v-click>

---

## ØVELSE: Datastrukturer i Python

Udled relevante oplysninger af nedenstående sætninger og sæt dem i en datastruktur, som du selv synes giver mening. Man skal kunne kalde alle oplysninger frem ved at kalde èn variabel.

*For at blive klogere på deres kundebase, har SuperGroce ansat en konsulent til at observere, hvad kunderne køber i deres supermarked. Der blev observeret følgende:*
    
> Emily, en 32-årig grafisk designer, fyldte sin kurv med avocadoer, mandelmælk, grønkål, quinoa og mørk chokolade, mens hendes loyale golden retriever, Max, tålmodigt ventede ved hendes side.

> Anders, en 45-årig arkæolog, købte fin-spidsede penne, kaffebønner, pitabrød og hummus, mens han forestillede sig sin aften med forskning sammen med sin nysgerrige papegøje, Luna.

> 60-årig pensionist Eleanor samlede i sin kurv tomater, mozzarella, basilikum, olivenolie og baguetter for at skabe hendes signaturret, caprese-salat, alt imens hendes kat, Whiskers, slappede af i hendes indkøbsvogn.

> Alex, en 19-årig universitetsstuderende, fyldte op med instant nudler, energidrikke, mikrobølgepopcorn, peanutbutter og brød. Sene studie-sessioner og hans stille guldfisk, Bubbles, ventede hjemme på kollegieværelset.

> Kokken Ramirez, en 50-årig kulinarisk ekspert, gik gennem gangene og valgte frisk basilikum, modne tomater, hvidløg, pasta og olivenolie for at tilberede en skøn pastaret, alt imens hans frække kæledyrsilder, Tango, kiggede ud fra hans skuldertaske.

> Sarah, en 25-årig romanforfatter, overvejede sine plot-ideer, mens hun valgte sort te, honning, mandler, blåbær og mørk chokolade, forestillede sig en hyggelig skrive-session forude, med hendes pjuskede kæledyrskat, Oliver, puttet op tæt ved.

---

## ØVELSE: Datastrukturer i Python

Udled af data hvilke kæledyr personerne over 40 år har.

---

# Opsummering

- Data kan struktureres i forskellige formater og strukturer
    - *Relationel* datastruktur er data i tabeller, som er begrænset til to dimensioner
    - *Hierarkisk* datastruktur er data i træ-lignende struktur
    - Valg af datastruktur hænger sammen med, hvad data skal bruges til