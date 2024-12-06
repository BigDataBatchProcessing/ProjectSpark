# Zestaw 7 – carstrucks-data

## Misja główna

### Cel przetwarzania 

Dla każdego producenta należy wyznaczyć: 
- stan o najwyższej średniej cenie samochodów. 
- dominujący kolor samochodów producenta w tym stanie 
- średnią cenę samochodów producenta w tym stanie 
- liczbę samochodów sprzedanych w tym stanie 
- listę kolorów, na które pomalowane były samochody producenta w tym stanie 

Podczas analiz uwzględniamy tylko te samochody, których cena oscylowała w przedziale pomiędzy 10-tym percentylem a 90-tym percentylem wyznaczonych na całym zbiorze danych. Do obliczania percentyli nie stosujemy obliczeń przybliżonych. 

Przy określaniu stanu dla danego producenta, nie bierzemy pod uwagę tych, w których nie przekroczył pułapu 99 sprzedanych samochodów (niezależnie od ich ceny) w żadnym z regionów tego stanu. 

Ostateczny wynik przetwarzania powinien zawierać następujące atrybuty: 
- `state` – symbol stanu o najwyższej średniej cenie samochodów producenta
- `manufacturer` – nazwa producenta 
- `dominant_color` – kolor dominujący (liczba sprzedanych samochodów o tym kolorze była największa)
- `avg_price` – średnia cena sprzedanych samochodów
- `cars` – liczba sprzedanych samochodów
- `colors` – lista kolorów, na które pomalowane były samochody 

Sugerowany schemat wyniku:
```
root
 |-- state: string (nullable = true)
 |-- manufacturer: string (nullable = true)
 |-- dominant_color: string (nullable = true)
 |-- avg_price: string (nullable = true)
 |-- cars: long (nullable = false)
 |-- colors: array (nullable = false)
 |    |-- element: string (containsNull = false)
```

Uwagi:
- lista kolorów ma dotyczyć tylko tych samochodów, które były wykorzystane do wyliczenia średniej ceny dla producenta i stanu, 
- lista kolorów nie może zawierać duplikatów 

 
## Misje poboczne 

### Misja 1

Dla każdego wariantu skrzyni biegów wyznacz liczbę oferowanych samochodów, cenę najdroższego z nich, stosunek liczby samochodów zasilanych olejem napędowym (`diesel`) do całkowitej liczby samochodów. Ignorujemy te oferty, których liczba pustych wartości wśród atrybutów: `transmission`, `fuel`, `price`, `manufacturer` jest większa bądź równa 2. 

Wynik ma zawierać następujące kolumny:
- `transmission` – typ skrzyni biegów 
- `cars` – liczba samochodów 
- `price_max` – największa cena 
- `diesel_ratio` – stosunek liczby samochodów zasilanych olejem napędowym do całkowitej liczby samochodów

### Misja 2 
Dla każdego stanu wyznacz liczbę regionów, w których liczba oferowanych samochodów z automatyczną skrzynią biegów przekraczała 50%. Ponadto oblicz średnią cenę oferowanych w tych regionach samochodów oraz ich liczbę. Nie uwzględniaj samochodów, których status (`title_status`) jest inny niż `clean`. 

Wynik ma zawierać następujące kolumny:
- `state` – nazwa stanu 
- `regions` – liczba regionów
- `price_avg` – średnia cena samochodów 
- `cars` – liczba samochodów
