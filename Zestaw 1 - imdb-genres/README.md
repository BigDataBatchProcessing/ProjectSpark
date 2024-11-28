# Zestaw 1 – imdb-genres

## Misja główna

### Cel przetwarzania 

Dla każdej dekady należy wyznaczyć trzy gatunki (`genres`) filmów mających wówczas premierę (`startYear`), w ramach których została zaangażowana największa sumaryczna liczba aktorów. Ograniczamy naszą analizę tylko do filmów długometrażowych (`titleType = 'movie'`) i występujących w nich aktorów. Nie należy uwzględniać gatunków, w ramach których więcej niż 50% wszystkich filmów (niezależnie od ich typu) przeznaczonych jest dla widzów dorosłych. 

Wynik przetwarzania powinien zawierać następujące atrybuty: 

- `decade` – dekada w formacie `RRR0`
- `genre` – gatunek 
- `movies` – liczba filmów długometrażowych
- `actors` – liczba aktorów w filmach długometrażowych

Sugerowany schemat wyniku:

```
root
 |-- decade: decimal(8,0) (nullable = true)
 |-- genre: string (nullable = false)
 |-- movies: long (nullable = false)
 |-- actors: long (nullable = false)
```

Uwagi:

- Filmy, które mają określonych wiele gatunków należy zaliczyć do każdego z nich
- Nie uwzględniamy filmów nie mających określonego żadnego gatunku oraz nie mających określonego roku premiery (akceptujemy tylko wartości, które są liczbami z przedziału 1800 i 2100) 
- Przez gatunek rozumiemy pojedynczy gatunek na liście gatunków określających charakter filmu, a nie ich złożenie (całą listę)
- Przez aktorów rozumiemy tylko te osoby, który oznaczone są jako aktorzy (`actor`), aktorki (`actress`), a także osoby, które zagrały samych siebie (`self`)
- Liczba filmów powinna obejmować wszystkie filmy z danego gatunku, nie tylko takie, w których występowali jacyś aktorzy
- Obliczając sumaryczną liczbę aktorów dla każdego gatunku i każdej dekady, nie liczymy wielokrotnie tych samych aktorów (np. jeśli występowali w wielu różnych filmach w ramach tego samego gatunku)

 
## Misje poboczne 

### Misja 1

Znajdź średnią długość filmów długometrażowych (`titleType = 'movie'`) dla kolejnych lat ich premiery. Ogranicz się tylko do tych lat, w których nakręcono co najmniej 1000 filmów. Wyniki posortuj chronologicznie. 

Wynik ma zawierać następujące kolumny:
- `startYear` – rok premiery 
- `avgRuntime` – średnia długość filmów 

### Misja 2

Dla każdego typu filmu wyznacz: 

- nazwę typu, 
- liczbę filmów, 
- liczbę aktorów (`category in ('actor', 'actress', 'self')`), którzy zagrali w tych filmach, 
- średnią długość filmów. 

Pomiń te typy filmów, dla których liczba filmów nie przekracza 100. 

Wynik ma zawierać kolumny

- `titleType` – typ filmu 
- `movies` – liczba filmów 
- `actors` – liczba aktorów 
- `avgRuntime` – średnia długość filmów 
