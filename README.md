# API Authentication Testing – Postman Collection

## Opis projektu

Projekt zawiera testy API skupione na mechanizmach uwierzytelniania (authentication) i autoryzacji (authorization).  
Testy zostały przygotowane w Postmanie na podstawie publicznego API Restful Booker.

Celem było sprawdzenie, czy:
- użytkownik może się poprawnie zalogować i otrzymać token,
- dostęp do endpointów jest ograniczony do użytkowników posiadających autoryzację,
- API poprawnie reaguje na brak lub niepoprawne dane uwierzytelniające.

---

## Zakres testów

### Logowanie
- poprawne dane → status 200, zwrócony token  
- niepoprawny login → status 401  
- niepoprawne hasło → status 401  

### Operacje wymagające autoryzacji
- wykonanie operacji (PUT, DELETE) z poprawnym tokenem  
- próba wykonania operacji bez tokena → status 403  
- próba wykonania operacji z niepoprawnym tokenem → status 403  

---

## Sposób działania

1. Wysłanie requestu logowania (`POST /auth`)
2. Pobranie tokena z odpowiedzi i zapisanie go do zmiennej kolekcji
3. Wykorzystanie tokena w nagłówku `Authorization` przy kolejnych requestach
4. Walidacja odpowiedzi API (statusy HTTP, struktura odpowiedzi)

---

## Uwagi

- API wykorzystuje uproszczony mechanizm autoryzacji – token przekazywany jest w nagłówku `Authorization` jako `Basic`, co nie jest standardowym podejściem (w praktyce stosuje się najczęściej Bearer token).
- Testy korzystają z istniejących danych (stałe ID zasobów), co może wpływać na ich stabilność w zależności od stanu środowiska.
- Projekt skupia się na pokazaniu sposobu testowania mechanizmów auth, a nie na pełnej walidacji bezpieczeństwa API.

---

## Wnioski

Testy pozwalają zweryfikować podstawowe scenariusze związane z autoryzacją oraz pokazują, jak API reaguje na brak lub błędne dane uwierzytelniające.  
Jednocześnie widoczne jest, że mechanizm autoryzacji w testowanym API jest uproszczony i nie w pełni odzwierciedla rozwiązania stosowane w systemach produkcyjnych.
