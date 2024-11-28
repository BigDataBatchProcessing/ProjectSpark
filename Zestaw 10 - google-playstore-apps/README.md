# Zestaw 10 – google-playstore-apps

## Misja główna

### Cel przetwarzania

Dla każdego roku wydawania aplikacji należy wyznaczyć nazwy trzech developerów, których aplikacje zostały zainstalowane przez największą sumaryczną liczbę użytkowników. Do analiz uwzględniamy tylko darmowe aplikacje ocenione przez co najmniej 1000 osób. Uwzględniamy tylko tych developerów, którzy wydali w danym roku co najmniej 5 aplikacji.

W rankingach uwzględniamy tylko tych developerów, dla których sumaryczna liczba instalacji (wszystkich aplikacji, niezależnie od ich oceny, liczby ocen oraz ceny) jest większa niż średnia sumaryczna liczba instalacji dla wszystkich developerów. 

Ostateczny wynik powinien zawierać następujące atrybuty: 
- `year` – rok wydania aplikacji 
- `developer_name` – nazwa developera
- `avg_rate` – średnia ocena użytkowników obejmująca oceny wszystkich aplikacji developera (nie może to być średnia średnich)
- `count_apps` – liczba aplikacji 
- `count_rates` – liczba ocen  
- `sum_installs` – sumaryczna liczba instalacji 
- `categories` – lista kategorii 

Sugerowany schemat wyniku:
```
root
 |-- year: integer (nullable = true)
 |-- developer_name: string (nullable = true)
 |-- avg_rate: double (nullable = true)
 |-- count_apps: long (nullable = false)
 |-- count_rates: long (nullable = true)
 |-- sum_installs: string (nullable = true)
 |-- categories: array (nullable = false)
 |    |-- element: string (containsNull = false)
```

Uwagi:
- Przemyśl to w jaki sposób wyznaczysz średnią ocen.
- Lista kategorii nie może zawierać duplikatów 
- Lista kategorii ma obejmować jedynie te aplikacje, które zostały uwzględnione w wynikach analizy
- Wartości w polu Category w źródłowych danych traktujemy jako pojedyncze atomowe, wartości. Przykładowo: Travel & Local to jedna wartość, a nie dwie.  
- Uważaj na pole Installs  zawierające liczbę instalacji. Ma ono dane w postaci `XXX,XXX,XXX+` lub `~` oraz `null`. Znak `~` oraz `null` traktujemy jako `0`, wszystkie pozostałe mają znaczenie wynikające z ich wartości. Znak `+` ignorujemy. 
 
## Misje poboczne 

### Misja 1
Wyznacz trzy kategorie aplikacji, które oceniane są najlepiej. Pomiń te kategorie, dla których powstało mniej niż 100 aplikacji. Oprócz średniej oceny, wyznacz liczbę aplikacji, liczbę developerów, liczbę aplikacji bezpłatnych (wykorzystaj kolumnę `Free`). 

Wynik ma zawierać następujące kolumny:
- `Category` – kategoria aplikacji 
- `avgRating` – średnia ocena aplikacji (pamiętaj o uwzględnieniu wag ocen) 
- `noApps` – liczba aplikacji 
- `noDevs` – liczba developerów 
- `noFreeApps` – liczba bezpłatnych aplikacji 

### Misja 2
Dla każdego developera, który wydawał aplikacje w latach 2019-2020 określ ile było tych aplikacji, ile różnych kategorii obejmowały te aplikacje, ile z nich było darmowych, jaka była średnia ich cena. 
Pomiń takich developerów, którzy wydali w tych latach mniej niż 5 aplikacji. 

Wynik ma zawierać następujące kolumny:
- `developerName` – nazwa developera
- `noApps` – liczba aplikacji 
- `noCategories` – liczba różnych gatunków 
- `noFreeApps` – liczba bezpłatnych aplikacji 
- `avgPrice` – średnia cena 
 