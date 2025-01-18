# Kryteria oceny

## Wprowadzenie 

Projekt dla każdego z API wymaga implementacji obejmującej:

* albo **misję główną** - wymagającą dokonywania złożonego przetwarzania danych
* albo **dwie misje poboczne** - dwa zadania o znacznie mniejszym poziomie złożoności 


## Kryteria oceny dla misji głównej 

Za implementację misji głównej dla każdego z API można otrzymać: 
* 6 punktów za poprawne rozwiązanie 
* 4 punkty za wysoką wydajność rozwiązania 


### Ocena poprawnego rozwiązania 

Ocena poprawnego rozwiązania dokonywana jest na podstawie następujących zasad:
- 0 pkt - brak implementacji lub implementacja nie działająca
- 1 pkt - brak zachowania czystości API - "za dobre chęci" 
- 2 pkt - zachowana czystość API, wynik odmienny od sugerowanego (akceptowanego)
- 5 pkt - zachowana czystość API, wynik w pełni zgodny z sugerowanym, niepoprawne miejsce docelowe 
- 6 pkt - zachowana czystość API, wynik w pełni zgodny z sugerowanym, poprawne miejsce docelowe

Przez brak czystości rozumiemy dowolny fragment przetwarzania wykraczający poza wyznaczone API 
- począwszy od zdefiniowania źródeł danych z użyciem właściwego kontekstu, 
- aż do uzyskania końcowego wyniku czyli
    - zapisania go do miejsca docelowego - w przypadku *RDD API* oraz *DataFrame API*
    - pobrania do lokalnej zmiennej (*Dataset API*, *Pandas API on Spark*) celem utworzenia lokalnego pliku JSON

Wybrane najczęstsze przykłady braku czystości:
- w *RDD API* skorzystanie z funkcjonalności *DataFrame API* podczas utworzenia źródła
- w *Dataset API* skorzystanie z dowolnej z metod *Untyped transformations* (https://spark.apache.org/docs/latest/api/scala/org/apache/spark/sql/Dataset.html) 
- w *Pandas API on Spark* skorzystanie z *Pandas API*.

Niepoprawne miejsce docelowe zwykle odnosi się do *DataFrame API*. Przykładowo, nie każda tabela zapisywana przez Apache Spark jest tabelą *Delta Lake*. 

Czasami ten sam problem dotyczy *Dataset API*/*Pandas API on Spark* - plik JSON lub katalog z plikami JSON w HDFS nie jest oczywiście lokalnym plikiem JSON. Przez lokalny plik JSON rozumiemy plik w lokalnym systemie plików (np. serwera master klastra).

### Punkty za wysoką wydajność rozwiązania 

Punkty za wysoką wydajność rozwiązania wynikają z metryk przetwarzania i możliwe są tylko w przypadku w pełni poprawnych rozwiązań (ocenionych na 6 punktów).

Do ich określenia służy poniższy wzór:

```
shuffleReadBytes + shuffleWriteBytes + inputBytes
```

Liczba punktów wynika z wartości wyznaczanej przez powyższy wzór zgodnie z poniższymi zasadami:

- 4 pkt - wartość nie większa niż wartość odniesienia 
- 3 pkt - wartość nie większa niż dwukrotność wartości odniesienia 
- 2 pkt - wartość nie większa niż czterokrotność wartości odniesienia
- 1 pkt - wartość nie większa niż ośmiokrotność wartości odniesienia
- 0 pkt - wartość większa niż ośmiokrotność wartości odniesienia

***Wartością odniesienia jest wartość najlepszego uzyskanego wyniku pomnożona razy 2***

Wartości odniesienia oczywiście są określane (są różne) dla każdego API i każdego zestawu.

#### Najlepsze wyniki 

##### Python

|Zestaw                           |Spark Core (RDD) |Spark SQL (DataFrame) |Pandas API on Spark |
|---------------------------------|----------------:|---------------------:|-------------------:|
|Zestaw 1 – imdb-genres           |   2,870,007,557 |        3,579,241,383 |      6,703,079,169 |
|Zestaw 2 – nyc-taxi              |   1,566,758,042 |        4,274,941,722 |      3,490,888,005 |
|Zestaw 3 – nyc-accidents         |     316,570,024 |          692,511,476 |      3,201,067,288 |
|Zestaw 4 – imdb-persons          |   4,858,225,869 |        6,051,322,783 |     14,234,179,376 |
|Zestaw 6 – fifa-players          |      51,049,470 |          192,387,830 |        630,129,140 |
|Zestaw 7 – carstrucks-data       |     103,477,904 |          337,395,846 |      1,040,571,615 |
|Zestaw 8 – flight-delays         |     632,588,852 |        1,191,963,494 |      2,383,908,271 |
|Zestaw 9 – discogs               |     982,114,075 |        2,099,330,761 |      3,398,451,443 |
|Zestaw 10 – google-playstore-apps|     732,019,809 |        1,295,625,331 |      2,643,834,438 |


##### Scala

| Zestaw                           | RDD API    | DataFrame API  | Dataset API  |
|----------------------------------|------------|----------------|--------------|
| Zestaw 1 - imdb-genres           | Dane 1-2   | Dane 1-3       | Dane 1-4   |
| Zestaw 2 - nyc-taxi              | Dane 2-2   | Dane 2-3       | Dane 2-4   |
| Zestaw 3 - myc-accidents         | Dane 3-2   | Dane 3-3       | Dane 3-4   |
| Zestaw 4 - imdb-persons          | Dane 4-2   | Dane 4-3       | Dane 4-4   |
| Zestaw 5 - netflix-prize-data    | Dane 5-2   | Dane 5-3       | Dane 5-4   |
| Zestaw 6 - fifa-players          | Dane 6-2   | Dane 6-3       | Dane 6-4   |
| Zestaw 7 - carstrucks-data       | Dane 7-2   | Dane 7-3       | Dane 7-4   |
| Zestaw 8 - flights-data          | Dane 8-2   | Dane 8-3       | Dane 8-4   |
| Zestaw 9 - discogs-data          | Dane 9-2   | Dane 9-3       | Dane 9-4   |
| Zestaw 10 - google-paystore-apps | Dane 10-2  | Dane 10-3      | Dane 10-4  |


## Kryteria oceny dla misji pobocznych 

Za obie misje poboczne, dla każdego API można otrzymać maksymalnie 5 punktów.

Przy czym, maksymalna liczba punktów za każdą z misji jest następująca:
- 2 pkt - za misję 1 
- 3 pkt - za misję 2  

Jeśli którekolwiek z rozwiązań nie zachowuje czystości kodu wówczas za oba (razem) rozwiązania należy się co najwyżej 1 pkt (za dobre chęci) 

Ocena za każdą misję jest uznaniowa 
- od 0 - sytuacja ekstremalna, niedziałający kod, lub rozwiązanie znacząco odbiegające od poprawnego, 
- do maksymalnej liczby punktów dla danej misji w przypadku rozwiązania w pełni poprawnego. 

Ocena obu misji poprawności polega na analizie kodu oraz faktu jego działania. 

