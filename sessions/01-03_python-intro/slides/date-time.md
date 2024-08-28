# Datoer og tid i Python

## Datoer og tid i Python

Indtil Python er fortalt andet, er datoer også blot strings

En dato giver ikke sig selv! Overvej fx en dato skrevet: "07/08/12"

    - 12. august 2007?
    - 7. august 2012?
    - 8. december 2007?
    - 8. juli 2012?

Python skal derfor informeres om et dato- og tidsformat, for at kunne behandle noget som tid

- `datetime` objekt (year, month, date, hour)
- `timedelta` objekt (days)

## Fra dato-string til dato-objekt

Basismodulet `datetime` kan bruges til at arbejde med datoer og tid.


```python
from datetime import datetime

now = datetime.now()
print(now)
```

    2022-09-11 22:30:39.807528


Fra et `datetime` objekt kan hvert enkelt tidsenhed tilgås som attribute:


```python
print(
    now.year,
    now.month,
    now.day,
    now.hour,
    now.minute,
    now.second,
    sep = "\n"
)
```

    2022
    9
    11
    22
    30
    39


## Fra dato-string til dato-objekt

Funktionen `datetime.strptime()` bruges til at konvertere en string til et datetime-objekt.


```python
datestring = "12/09-22"
date = datetime.strptime(datestring, "%d/%m-%y")

print(date)
```

    2022-09-12 00:00:00


Python fortælles datoformatet via en række specialtegn (`%d`, `%m`, `%Y` osv.).

**Eksempler:**

|Tegn|Betydning|Eksempel|
|--|--|--|
|`%d`|Dag i måneden (tocifret)|04, 10, 21|
|`%m`|Månede som tal (tocifret|02, 06, 11|
|`%b`|Forkortet måned (baseret på sprogindstilling)|Jan, Mar, Jun|
|`%y`|Tocifret årstal|88, 99, 22|
|`%Y`|Firecifret årstal|1988, 1999, 2022|

<table>
<thead>
<tr><th>Tegn</th><th>Betydning</th><th>Eksempel</th></tr></thead>
<tbody><tr><td><code>%d</code></td><td>Dag i måneden (tocifret)</td><td>04, 10, 21</td></tr><tr><td><code>%m</code></td><td>Månede som tal (tocifret</td><td>02, 06, 11</td></tr><tr><td><code>%b</code></td><td>Forkortet måned (baseret på sprogindstilling)</td><td>Jan, Mar, Jun</td></tr><tr><td><code>%y</code></td><td>Tocifret årstal</td><td>88, 99, 22</td></tr><tr><td><code>%Y</code></td><td>Firecifret årstal</td><td>1988, 1999, 2022</td></tr></tbody>
</table>

Se oversigt over formatkoder her: https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior

## Tidsdifferencer

- Python kan arbejde med tidsdifferencer
- Ved at udregne differnece baseret på to datetime-objekter, dannes et "timedelta" objekt:


```python
date1 = datetime.strptime('01-09-2022', '%d-%m-%Y').date()
datenow = datetime.now().date()

timedif = datenow - date1

timedif.days
```




    10



## Datetime i pandas

Pandas indeholder en del metoder til at arbejde med datetime, der minder om basismodulet
- Tilgås under `.dt`

For at konvertere en data frame kolonne til dato, bruges funktionen `pd.to_datetime()` (fungerer meget ligesom `datetime.strptime()`
- *Bemærk*: Funktion; ikke metode. Tager en Series med datolignende strings og datoformat som argument


```python
dates = pd.Series(["2022-08-02", "2022-08-04", "2022-06-30"])

dates = pd.to_datetime(dates, format = "%Y-%m-%d")

print(dates)
```

    0   2022-08-02
    1   2022-08-04
    2   2022-06-30
    dtype: datetime64[ns]


Efter at kolonnen er konverteret, kan datetime-metoderne under `.dt` tilgås:


```python
print(dates.dt.day)
```

    0     2
    1     4
    2    30
    dtype: int64


# Datoer og tid i Python (live-coding)

## FÆLLES ØVELSE: Datoer og tid i Python

I Eurobarometer-datasættet indeholder kolonnen `p1` datoen for dataindsamlingen for respondenten.

Hvordan kan det undersøges, hvor lang tid det tog at samle data fra de danske respondenter?

## Opsummering

- Datoer i Python er strings, indtil Python er fortalt andet
- `datetime` modulet bruges til at konvertere strings til datoer *uden for pandas*
    - I pandas bruges `pd.to_datetime()`
