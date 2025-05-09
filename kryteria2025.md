# Kryteria oceny

## Wprowadzenie 

Projekt dla każdego z API wymaga implementacji obejmującej:

* albo **misję główną** - wymagającą dokonywania złożonego przetwarzania danych
* albo **dwie misje poboczne** - dwa zadania o znacznie mniejszym poziomie złożoności 


## Kryteria oceny dla misji głównej 

Za implementację misji głównej dla każdego z API można otrzymać: 
* 8 punktów za poprawne rozwiązanie 
* 2 punkty za wysoką wydajność rozwiązania 


### Ocena poprawnego rozwiązania 

Ocena poprawnego rozwiązania dokonywana jest na podstawie następujących zasad:
- 0 pkt - brak implementacji lub implementacja, która nie działa
- 2 pkt - brak zachowania czystości API - "za dobre chęci" 
- 4 pkt - zachowana czystość API, wynik odmienny od sugerowanego (akceptowanego)
- 6 pkt - zachowana czystość API, wynik w pełni zgodny z sugerowanym, niepoprawne miejsce docelowe 
- 8 pkt - zachowana czystość API, wynik w pełni zgodny z sugerowanym, poprawne miejsce docelowe

Przez brak czystości rozumiemy dowolny fragment przetwarzania wykraczający poza wyznaczone API 
- począwszy od zdefiniowania źródeł danych z użyciem właściwego kontekstu, 
- aż do uzyskania końcowego wyniku czyli
    - zapisania go do miejsca docelowego - w przypadku *RDD API* oraz *DataFrame API*
    - pobrania do lokalnej zmiennej (*Dataset API*, *Pandas API on Spark*) celem utworzenia lokalnego pliku JSON

Wybrane najczęstsze przykłady braku czystości:
- w *RDD API* skorzystanie z funkcjonalności *DataFrame API* podczas utworzenia źródła
- w *Pandas API on Spark* skorzystanie z *Pandas API*.

Niepoprawne miejsce docelowe zwykle odnosi się do *DataFrame API*. Przykładowo, nie każda tabela zapisywana przez Apache Spark jest tabelą *Delta Lake*. 

Czasami ten sam problem dotyczy *Pandas API on Spark* - plik JSON lub katalog z plikami JSON w HDFS nie jest oczywiście lokalnym plikiem JSON. Przez lokalny plik JSON rozumiemy plik w lokalnym systemie plików (np. serwera master klastra). 
Sam wynik w tym przypadku może być utworzony na poziomie sterownika z użyciem jezyka Python o ile ostateczny wynik zapisywany do tego pliku został uzyskany zgodnie z wymaganym API. 

### Punkty za wysoką wydajność rozwiązania 

Punkty za wysoką wydajność rozwiązania wynikają z analizy kodu i możliwe są do uzyskania tylko w przypadku w pełni poprawnych rozwiązań (ocenionych na 8 punktów).

Zasady przyznawania punktów za wydajność są następujące:

- ***RDD API*** - (1) brak wielokrotnego odwoływania się do źródeł danych oraz (2) zastosowanie wielopoziomowych agregacji ograniczających ilość przesyłanych danych (*shuffling*)
- ***DataFrame API*** - (1) brak wielokrotnego odwoływania się do źródeł danych oraz (2) wykonanie całości z wykorzystaniem jednej akcji (jednego zapytania)  
- ***Pandas API*** - tu sam fakt poprawnego rozwiązania pozwala na przyznanie kompletu punktów za wydajność

Liczba punktów wynika z liczby spełnionych powyżej zasad.



## Kryteria oceny dla misji pobocznych 

Za misje poboczne można otrzymać następującą maksymalną liczbę punktów:
- 2 pkt - za misję 1 
- 3 pkt - za misję 2  

Za obie misje poboczne, dla każdego API można otrzymać maksymalnie 5 punktów.

Jeśli którekolwiek z rozwiązań nie zachowuje czystości kodu wówczas za oba (razem) rozwiązania należy się co najwyżej 1 pkt (za dobre chęci).

Ocena za każdą misję jest uznaniowa 
- od 0 - sytuacja ekstremalna, niedziałający kod, lub rozwiązanie znacząco odbiegające od poprawnego, 
- do maksymalnej liczby punktów dla danej misji w przypadku rozwiązania w pełni poprawnego. 

Ocena poprawności obu misji polega na analizie kodu oraz faktu jego działania. 

