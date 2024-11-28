# Zestaw 5 – netflix-prize-data

### Cel przetwarzania

Należy, dla każdej dekady produkcji filmów, wyznaczyć trzy najlepiej oceniane filmy (o największej średniej ocenie) pod warunkiem, że zostały one ocenione przez co najmniej 1000 osób.

W obliczeniach nie chcemy uwzględniać ocen tych użytkowników, którzy wystawili tylko jedną ocenę. 

Ponadto, nie chcemy uwzględniać ocen, które zostały wystawione przed datą ukazania się filmów. 

Ostateczny wynik (6) powinien zawierać następujące atrybuty: 
- `tytul_filmu` – tytuł filmu
- `dekada_produkcji` – dekada produkcji filmu
- `srednia_ocena` – średnia ocena filmu
- `liczba_ocen` – liczba ocen filmu
- `3top_dni` – trzy dni, w których wystawiono największą liczbę ocen 

