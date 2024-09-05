## Sammensætning af data

Man kan af forskellige årsager have behov for at sammensætte datasæt. 

Man adskiller typsik mellem at udvide med flere *observationer* eller med flere *variable/oplysninger*.

**Udvide med flere observationer**
- Data indsamlet over flere omgange
- Løbende opdatering af data

**Udvide med flere variable/oplysninger**
- Data samles på tværs af flere kilder
- Oplysninger på forskellige enhedsniveauer

---

## Udvid med flere observationer - appending/concatenating

At udvide data med flere observationer kaldes typisk *appending* eller *concatenating* (for tabulær data).

Bruges typisk når datasæt har samme kolonner, men forskellige rækker.

![concat](https://pandas.pydata.org/pandas-docs/stable/_images/merging_concat_basic.png){width=35% lazy}

*Source: pandas.pydata.org/*

---

## Udvid med flere variable/oplysninger - join/merge

At udvide data med flere variable/oplysninger kaldes typisk for *join* eller *merge* (for tabulær data).

Bruges typisk når datasæt deler nogle af de samme observationer, men har forskellige variable/oplysninger.

Man *joiner* typisk to datasæt ad gangen. De to datasæt, som joines, kaldes typisk *left* og *right* (terminologien kommer fra SQL - et databasesprog).

Datasæt joines ud fra en eller flere *nøglevariable* - noget som unikt identificerer observationen/enheden.

![join](https://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key.png)

*Source: pandas.pydata.org/*

---

## Typer af joins

![join-types](https://learnsql.fr/blog/comment-apprendre-les-jointures-sql/2.png){width=70% lazy}

*Source: learnsql.fr*

---
layout: section
---

# Dataformater (wide-long)

---

## Dataformater (wide-long)

Datasæt kan have forskellige formater og strukturer. Det kan ofte være nødvendigt at ændre på datas format - enten for at det passer med den metode/funktion/model, som det skal bruges i, eller fordi det skal sættes sammen med andre datasæt.

For datasæt i en tabelstruktur (rækker og kolonner), kan man overordnet adskille mellem to formater:
- wide: én række per observeret enhed (fx person), hvor hver oplysning/variabel har sin egen kolonne
- long: en observeret enhed kan have flere rækker, hvor en variabel indikerer, hvilken oplysning der er tale om for enheden

Man støder ofte på det ene eller andet format i forbindelse med tidsserier, hvor man har gentagne målinger for de samme enheder. 


---

## Dataformater (wide-long)

```python
# code for generating examples
import pandas as pd
import random

wide_df = pd.DataFrame({'person': ['A', 'B', 'C'],
                        '2010': random.sample(range(0,100), 3),
                        '2011': random.sample(range(0,100), 3),
                        '2012': random.sample(range(0,100), 3),
                       }
                      )

wide2_df = pd.DataFrame({'person': ['A', 'B', 'C', 'D'],
                         'age': [22, 53, 36, 42],
                         'car_colour': ['red', 'white', 'blue', 'orange']
                        }
                       )

long_df = pd.melt(wide_df, id_vars = ['person'], var_name = 'year', value_name = 'train_rides')
long2_df = pd.melt(wide2_df, id_vars = ['person'], var_name = 'variable', value_name = 'value')
```

---

### Fra wide til long - eksempel 1


```python
wide_df
```

|      | person | 2010 | 2011 | 2012 |
| ---- | ------ | ---- | ---- | ---- |
| 0    | A      | 32   | 16   | 30   |
| 1    | B      | 83   | 37   | 8    |
| 2    | C      | 8    | 55   | 55   |


---

### Fra wide til long - eksempel 1

```python
long_df
```

|      | person | year | train_rides |
| ---- | ------ | ---- | ----------- |
| 0    | A      | 2010 | 32          |
| 1    | B      | 2010 | 83          |
| 2    | C      | 2010 | 8           |
| 3    | A      | 2011 | 16          |
| 4    | B      | 2011 | 37          |
| 5    | C      | 2011 | 55          |
| 6    | A      | 2012 | 30          |
| 7    | B      | 2012 | 8           |
| 8    | C      | 2012 | 55          |

---

### Fra wide til long - eksempel 2


```python
wide2_df
```

|      | person | age  | car_colour |
| ---- | ------ | ---- | ---------- |
| 0    | A      | 22   | red        |
| 1    | B      | 53   | white      |
| 2    | C      | 36   | blue       |
| 3    | D      | 42   | orange     |

---

### Fra wide til long - eksempel 2

```python
long2_df
```

|      | person | variable   | value  |
| ---- | ------ | ---------- | ------ |
| 0    | A      | age        | 22     |
| 1    | B      | age        | 53     |
| 2    | C      | age        | 36     |
| 3    | D      | age        | 42     |
| 4    | A      | car_colour | red    |
| 5    | B      | car_colour | white  |
| 6    | C      | car_colour | blue   |
| 7    | D      | car_colour | orange |


---
layout: center
---

# Sammensætning af data og ændring af dataformat (live-coding)

---

# Opsummering

- Datasæt kan sammensættes på forskellig vis
    - Sammensætning af *rækker* kaldes typisk *appending* eller *concatenating* for tabulær data
    - Sammensætning af *varible* kaldes typisk *join* eller *merge* for tabulær data
- Tabulær data kan være i forskellige formater
    - Data i *wide* format indeholder én række per enhed
    - Data i *long* format kan indeholde flere rækker per enhed (fx ved tidsserier)
