# Zestaw 3 – nyc-accidents

## Misja główna

### Cel przetwarzania

Dla każdego typu poszkodowanych należy wyznaczyć ulice (fragmenty) leżące na terenie dzielnic, dla których sumaryczna liczba wypadków jest większa niż średnia liczba wypadków dla wszystkich dzielnic. Lista ulic dla każdego typu poszkodowanych ma być ograniczona do trzech, dla których suma poszkodowanych (zabici+ranni) jest największa. Wyniki analizy mają uwzględniać tylko do wypadki mające miejsce po 2012 roku i opisane kodem pocztowym występującym w zbiorze zawierającym listę kodów pocztowych.

Wynik przetwarzania powinien zawierać następujące atrybuty: 

- `street` – ulica
- `borough` – dzielnica, na terenie której znajduje się ulica
- `person_type` – typ poszkodowanych
- `killed` – liczba zabitych
- `injured` – liczba rannych

Sugerowany schemat wyniku 
```
root
 |-- street: string (nullable = true)
 |-- borough: string (nullable = true)
 |-- person_type: string (nullable = false)
 |-- injured: double (nullable = true)
 |-- killed: double (nullable = true)
```

Uwagi:
- Nie modyfikujemy nazw ulic, różniące się nazwy ulic powinny być obsługiwane niezależnie, jako różne ulice
- Każde zdarzenie może być opisane trzema różnymi ulicami. W zależności od tego ile ulic zostało określonych, dane zdarzenie należy zaliczyć na konto każdej z nich. 
- Wypadki mające miejsce na ulicach leżących na terenie kilku dzielnic rozważamy zgodnie z ich kodem pocztowym (ta sama ulica może być uwzględniana w ramach wielu dzielnic)

 
## Misje poboczne 

### Misja 1

Dla każdego dnia tygodnia wyznacz liczbę wypadków, sumę osób rannych (wykorzystaj numer_of_persons_injured), sumę osób zabitych (wykorzystaj numer_of_persons_killed). 
Pomijaj te wypadki, w których ze wszystkich trzech ulic określona jest tylko off_street_name. 
Wyniki uporządkuj pod względem liczby wypadków.

Wynik ma zawierać następujące kolumny

- `dayOfWeek` – dzień tygodnia 
- `crashesCount` – liczba wypadków 
- `injuried` – suma osób rannych 
- `killed` – suma osób zabitych 

### Misja 2

Dla trzech dzielnic o największej liczbie wypadków z udziałem pieszych wyznacz: liczbę wypadków z rannymi pieszymi, liczbę wypadków z zabitymi pieszymi, a także liczbę różnych kodów pocztowych, w których te wypadki wystąpiły. 
Pomiń te dzielnice, w których liczba poszkodowanych pierwszych była mniejsza od liczby poszkodowanych rowerzystów. 

Wynik ma zawierać kolumny:
- `borough` – nazwa dzielnicy
- `crashesWithInjuriesCount` – liczba wypadków z osobami rannymi 
- `crashesWithKilledCount` – liczba wypadków z osobami zabitymi 
- `distinctZipCodesCount` – liczba różnych kodów pocztowych
