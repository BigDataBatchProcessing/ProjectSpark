# Zestaw 8 – flight-delays

## Misja główna

### Cel przetwarzania 

Dla każdego miesiąca i roku należy wyznaczyć stan o największym średnim opóźnieniu przylotów (pozostałe miary, które należy wyliczyć są wymienione w opisie wyniku przetwarzania). Podczas obliczeń należy pominąć loty odwołane. Podczas obliczeń należy wyeliminować wpływ przylotów wykonanych przed czasem, takie przyloty należy traktować jako wykonane bez opóźnień (opóźnienie zerowe). Przy obliczaniu opóźnień przylotów należy uwzględniać tylko wartości w `ARRIVAL_DELAY`. 

W rankingach mają być brane pod uwagę tylko takie stany, dla których całkowita liczba lądowań jest powyżej średniej liczby lądowań dla wszystkich stanów. 

Ostateczny wynik przetwarzania powinien zawierać następujące atrybuty: 
- `year` – rok
- `month` – miesiąc
- `state` – nazwa stanu o największym średnim opóźnieniu przylotów
- `most_delayed_airline` – linia lotnicza z największym procentem przylotów opóźnionych (w ramach stanu, miesiąca i roku)
- `avg_delay` – średnie opóźnienie przylotów (w ramach stanu, miesiąca i roku)
- `percent` – procent przylotów opóźnionych (w ramach stanu, miesiąca i roku)
- `airlines` – lista linii lotniczych (w ramach stanu, miesiąca i roku)

Sugerowany schemat wyniku:
```
root
 |-- year: integer (nullable = true)
 |-- month: integer (nullable = true)
 |-- state: string (nullable = true)
 |-- most_delayed_airline: string (nullable = true)
 |-- avg_delay: double (nullable = true)
 |-- percent: double (nullable = true)
 |-- airlines: array (nullable = false)
 |    |-- element: string (containsNull = false)
```

Uwagi:
- lista linii lotniczych nie może zawierać duplikatów 
- lista linii lotniczych powinna uwzględniać tylko przyloty ujęte w obliczeniach (bez anulowanych) 

 
## Misje poboczne 

### Misja 1

Wyznacz trzy dni, w których odwołano największy procent lotów. Ponadto wylicz ile takich lotów zostało odwołanych. 

Wynik ma zawierać następujące kolumny:
- `day` – dzień w formacie `YYYY-MM-DD`
- `day_of_week` – dzień tygodnia 
- `cancellation_ratio` – procent odwołanych lotów 
- `cancelled_count` – liczba odwołanych lotów 

### Misja 2

Wyznacz trzy pary lotnisk, pomiędzy którymi wykonano największą liczbę lotów. Nie uwzględniaj lotów odwołanych. Oprócz liczby lotów wyznacz także: najmniejszą i największą odległość (distance) tych lotów oraz liczbę lotów przekierowanych.

Wynik ma zawierać następujące kolumny:
- `origin` – miejsce startu w formacie `airport (city, state)`
- `destination` – miejsce docelowe w formacie `airport (city, state)`
- `flights` – liczba lotów 
- `min_distance` – najmniejsza odległość
- `max_distance` – największa odległość
- `diverted_count` – liczba lotów przekierowanych 
