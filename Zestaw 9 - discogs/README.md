# Zestaw 9 – discogs

## Misja główna

### Cel przetwarzania 

Dla każdej dekady należy wyznaczyć trzy wytwórnie, które wydały największą liczbę płyt. Do obliczeń uwzględniamy tylko te płyty, które mają status Accepted. W rankingach nie uwzględniamy tych wytwórni, które ograniczają się do mniej niż pięciu różnych stylów muzyki na wydanych przez siebie płytach. 

Ostateczny wynik przetwarzania powinien zawierać następujące atrybuty: 
- `decade` – dekada w formacie `RRR0`
- `label_name` – nazwa wytwórni
- `artists_count` – liczba różnych artystów na wydanych płytach
- `releases_count` – liczba wydanych płyt
- `genres` – lista nazw różnych gatunków na wydanych płytach 
- `best_year` – rok  z największą liczbą wydanych płyt (w danej wytwórni i w danej dekadzie)

Sugerowany schemat wyniku
```
root
 |-- decade: integer (nullable = true)
 |-- label_name: string (nullable = true)
 |-- artists_count: long (nullable = false)
 |-- releases_count: long (nullable = false)
 |-- genres: array (nullable = false)
 |    |-- element: string (containsNull = false)
 |-- best_year: integer (nullable = true)
```

Uwagi:
- lista gatunków nie może zawierać duplikatów 
- lista gatunków ma uwzględniać gatunki tylko na płytach ujętych w obliczeniach 
- wartość w kolumnie `genre` w źródłowym zbiorze danych traktujemy jako jeden gatunek. 
  Przykładowo wartość `Folk, World, & Country` ma być traktowana jako jedna atomowa wartość.
 
## Misje poboczne 

### Misja 1

Dla podanych poniżej artystów podaj następujące informacje: liczba wydanych płyt, liczba wytwórni, w ramach których te płyty były wydane, przedział lat, w których pojawiały się te płyty, lista gatunków występujących na tych płytach.
Lista wykonawców: `U2`, `Dire Straits`, `Tom Waits`, `Maanam`, `Creedence Clearwater Revival`

Wynik ma zawierać następujące kolumny:
- `artist_name` – nazwa wykonawcy 
- `records` – liczba wydanych płyt
- `labels` – liczba wytwórni 
- `years` – przedział lat w ramach których wydane zostały płyty formacie YYYY-YYYY
- `genres` – lista gatunków 

### Misja 2 
Dla każdej wytwórni wyznacz liczbę współpracujących z nią wykonawców, którzy wydali w ramach tej wytwórni co najmniej 5 płyt. Nie uwzględniaj płyt, które w gatunku mają wskazane wartości Electronic i Classical. 
Oprócz liczby wykonawców podaj także liczbę wspomnianych płyt tych wykonawców wydanych na CD (format=CD) oraz liczbę płyt wydanych na winylu (format=Vinyl). 

Pomiń te wytwórnie, które współpracowały z mniej niż 50-oma powyżej scharakteryzowanymi wykonawcami. 

Wynik ma zawierać następujące kolumny:
- `label_name` – nazwa wytwórni
- `artists` – liczba wykonawców
- `CDs` – liczba płyt wydanych na CD
- `Vinyls` – liczba płyt wydanych na winylu 
