# Zestaw 4 – imdb-persons

## Misja główna

### Cel przetwarzania 

Dla czterech najbardziej popularnych profesji należy wyznaczyć trzy osoby, które były zaangażowane w największą liczbę filmów zgodnie z tą profesją. 
W obliczeniach nie uwzględniamy filmów, dla których nie ma zdefiniowanej "pełnej obsady". 

Film z pełną obsadą to taki, który posiada: 
- co najmniej jednego aktora (`role in (actor, actress, self)`), 
- co najmniej jednego reżysera (`role = director`) oraz 
- osoby pełniące co najmniej dwie inne dowolne role. 

Ostateczny wynik powinien zawierać następujące atrybuty: 
- `profession` – profesja
- `primaryName` – nazwa osoby
- `movies` – liczba filmów 

Sugerowany schemat wyniku 
```
root
 |-- profession: string (nullable = false)
 |-- primaryName: string (nullable = true)
 |-- movies: long (nullable = false)
```

Uwagi
- Przez profesje rozumiemy wartości występujące jako rozdzielane przecinkami składowe w `primaryProfession` wyłączając z nich wartość `"miscellaneous"`
- Poziom popularności profesji wyznaczany jest wyznaczany jest na podstawie tego ile osób posiada daną profesję na swojej liście profesji w `primaryProfession`
- Podczas porównywania roli osoby w filmie z jej podstawowymi profesjami sprawdzamy czy są one równe (bez semantycznych dodatkowych interpretacji np. traktujących rolę `self` jako profesję `actor` itp.)
 
## Misje poboczne 

### Misja 1
Przeanalizuj dane dotyczące zmarłych osób wyznacz ile osób żyło określoną liczbę lat. Podaj ilu z nich było aktorami, a ilu reżyserami. 

Wynik ma zawierać następujące kolumny:
- `age` – liczba przeżytych lat
- `persons` – liczba osób, które przeżyły określoną liczbę lat
- `actors` – liczba aktorów (`primaryProfession` zawiera jedną z wartości: `actors`, `actress`). 
- `directors` - liczba reżyserów (`primaryProfession` zawiera wartość `director`).

### Misja 2
Wśród osób, które urodziły się w ubiegłym wieku i które przeżyły ponad 70 lat, wyznacz te trzy, które za brały udział w największej liczbie filmów. Określ w ilu filmach byli oni aktorami oraz ile z tych filmów zostało przez nich wyreżyserowane. 

Wynik ma zawierać następujące kolumny:
- `primaryName` – nazwa (imię i nazwisko) osoby
- `birthYear` – data urodzenia 
- `age` – wiek 
- `filmCount` – liczba filmów w których osoba brała udział
- `filmCountAsActor` – liczba filmów, w których osoba była aktorem/aktorką (role in (`actors`, `actress`, `self`)). 
- `FilmCountAsDirector` - liczba filmów, w których osoba była reżyserem/reżyserką (`role` = `director`).


