# Sammensætning af data

## Sammensætning af data

Man kan af forskellige årsager have behov for at sammensætte datasæt. 

Man adskiller typsik mellem at udvide med flere *observationer* eller med flere *variable/oplysninger*.

**Udvide med flere observationer**
- Data indsamlet over flere omgange
- Løbende opdatering af data

**Udvide med flere variable/oplysninger**
- Data samles på tværs af flere kilder
- Oplysninger på forskellige enhedsniveauer

## Udvid med flere observationer - appending/concatenating

At udvide data med flere observationer kaldes typisk *appending* eller *concatenating* (for tabulær data).

Bruges typisk når datasæt har samme kolonner, men forskellige rækker.

![concat](https://pandas.pydata.org/pandas-docs/stable/_images/merging_concat_basic.png)

*Source: pandas.pydata.org/*

## Udvid med flere variable/oplysninger - join/merge

At udvide data med flere variable/oplysninger kaldes typisk for *join* eller *merge* (for tabulær data).

Bruges typisk når datasæt deler nogle af de samme observationer, men har forskellige variable/oplysninger.

Man *joiner* typisk to datasæt ad gangen. De to datasæt, som joines, kaldes typisk *left* og *right* (terminologien kommer fra SQL - et databasesprog).

Datasæt joines ud fra en eller flere *nøglevariable* - noget som unikt identificerer observationen/enheden.

![join](https://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key.png)

*Source: pandas.pydata.org/*

## Typer af joins

![join-types](https://learnsql.fr/blog/comment-apprendre-les-jointures-sql/2.png)

*Source: learnsql.fr*

# Dataformater (wide-long)

## Dataformater (wide-long)

Datasæt kan have forskellige formater og strukturer. Det kan ofte være nødvendigt at ændre på datas format - enten for at det passer med den metode/funktion/model, som det skal bruges i, eller fordi det skal sættes sammen med andre datasæt.

For datasæt i en tabelstruktur (rækker og kolonner), kan man overordnet adskille mellem to formater:
- wide: én række per observeret enhed (fx person), hvor hver oplysning/variabel har sin egen kolonne
- long: en observeret enhed kan have flere rækker, hvor en variabel indikerer, hvilken oplysning der er tale om for enheden

Man støder ofte på det ene eller andet format i forbindelse med tidsserier, hvor man har gentagne målinger for de samme enheder. 


```python
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

### Fra wide til long - eksempel 1


```python
wide_df
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
      <th>person</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>32</td>
      <td>16</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>83</td>
      <td>37</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>8</td>
      <td>55</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
long_df
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
      <th>person</th>
      <th>year</th>
      <th>train_rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>2010</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2010</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>2010</td>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A</td>
      <td>2011</td>
      <td>16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>B</td>
      <td>2011</td>
      <td>37</td>
    </tr>
    <tr>
      <th>5</th>
      <td>C</td>
      <td>2011</td>
      <td>55</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A</td>
      <td>2012</td>
      <td>30</td>
    </tr>
    <tr>
      <th>7</th>
      <td>B</td>
      <td>2012</td>
      <td>8</td>
    </tr>
    <tr>
      <th>8</th>
      <td>C</td>
      <td>2012</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>



### Fra wide til long - eksempel 2


```python
wide2_df
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
      <th>person</th>
      <th>age</th>
      <th>car_colour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>22</td>
      <td>red</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>53</td>
      <td>white</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>36</td>
      <td>blue</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>42</td>
      <td>orange</td>
    </tr>
  </tbody>
</table>
</div>




```python
long2_df
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
      <th>person</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>age</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>age</td>
      <td>53</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>age</td>
      <td>36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>age</td>
      <td>42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A</td>
      <td>car_colour</td>
      <td>red</td>
    </tr>
    <tr>
      <th>5</th>
      <td>B</td>
      <td>car_colour</td>
      <td>white</td>
    </tr>
    <tr>
      <th>6</th>
      <td>C</td>
      <td>car_colour</td>
      <td>blue</td>
    </tr>
    <tr>
      <th>7</th>
      <td>D</td>
      <td>car_colour</td>
      <td>orange</td>
    </tr>
  </tbody>
</table>
</div>



# Sammensætning af data og ændring af dataformat (live-coding)

# Opsummering

- Datasæt kan sammensættes på forskellig vis
    - Sammensætning af *rækker* kaldes typisk *appending* eller *concatenating* for tabulær data
    - Sammensætning af *varible* kaldes typisk *join* eller *merge* for tabulær data
- Tabulær data kan være i forskellige formater
    - Data i *wide* format indeholder én række per enhed
    - Data i *long* format kan indeholde flere rækker per enhed (fx ved tidsserier)
