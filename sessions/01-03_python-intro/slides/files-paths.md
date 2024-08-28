# Indlæsning af filer i Python

## Indlæsning af filer i Python

- Al indlæsning af filer i Python er baseret på *filstier*
- En *filsti* angiver placeringen af en fil på en computer (kaldt en *file path* på engelsk og omtales typisk *path* i programmering)
- En filsti angiver, hvordan computeren skal navigere igennem mapper (*directories*) for at finde en bestemt fil

## Indlæsning af filer i Python

**Absolutte filstier**

- Angiver *hele* filstien fra compuerens "rod" (*root*)

*Eksempler*: 
- Windows: `C:\Users\kgk\data\datafil.csv`
- Mac: `/Users/kgk/data/datafil.csv`
- Linux: `/usr/kgk/data/datafil.csv`

**Relative filstier**

- Angiver filstien fra *arbejssti* til filen
- *Arbejdssti* typisk den fil, som koden køres fra, men arbejdssti kan også ændres i koden
- `..`: Gå et niveau "op"
- `.`: Den nuværende directory

*Eksempel*: `../../data/datafil.csv`

## Filstier i Python

- Filstier angives blot som strings:

```python
path = "../../data/datafil.csv"
```

- Hvis en funktion forventer en filsti, skal denne blot angives som string:

```python
df = pd.read_csv(path)
```

## `os` modulet

`os` modulet indeholder (blandt andet) en række funktioner til at navigere i filsystemer
- `os.getcwd()` - print nuværende arbejdsmappe ("cwd": current working directory)
- `os.chdir()` - ændr arbejdsmappe 

`os` indeholder også funktionen `join` (`os.path.join()`). Denne gør det muligt at lave systemuafhængige filstier.
- Sti som string: `path = "../../data/datafil.csv"`
- Sti via `os`-modulet: `path = os.path.join("..", "..", "data", "datafil.csv")`


Fordi filstier i princippet blot er sammensatte strings, kan man med fordel arbejde med variable, der angiver placeringen til mapper, som bruges flere gange (fx datamappe, outputmappe eller andet):

```python
datadir = "../../data"
datafile = "datafil.csv"
datapath = os.path.join(datadir, datafile)
```

## `open` funktionen 

Hvordan filer indlæses i Python afhænger både af, hvilken filtype det er samt hvilken datastruktur, det skal læses ind i.

Funktionen `open` er en basisfunktion til at åbne tekstfiler i Python - enten til at skrive eller læse
1. Åben filen via filens sti
2. Angiv funktion(er) for at læse filen ind i korrekt datastruktur

```python
filepath = "../../data/tekstfil.txt"
fileconn = open(filepath, "r") # "r" angiver at filen åbnes i læsetilstand

with fileconn as f:
    data = f.read()
```

# Indlæsning af tekstfiler i Python (live-coding)

## Opsummering

- Al data indlæses via *filstier*
- `os` modulet bruges til at navigere i filsystemer
- `open` funktionen bruges til at åbne filer
