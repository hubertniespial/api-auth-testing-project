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

## Screenshoty

### Logowanie – poprawne dane
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/64402685-7139-48c5-a5b0-d003c9f18b3b" />
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/21a10b70-0713-46e3-ba8c-c10cac0b541b" />

### Logowanie – błędne dane
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/42182c54-1ad5-47ac-9b07-e48601c5af2d" />
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/c8a93683-c9bc-4b6d-b365-e5face82a6bb" />

### Operacja z poprawnym tokenem
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/feb1223e-fb78-4ff2-b6eb-e3f98d1ec34d" />

### Operacja bez tokena
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/67424c4b-0d58-439e-83c7-218b2161368e" />

### Operacja z niepoprawnym tokenem
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/2781f3da-559b-43dd-929d-4e8b6a119898" />
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/95a9c0af-34ca-40ad-a1f7-c43be703a0ce" />
<img width="1495" height="922" alt="image" src="https://github.com/user-attachments/assets/af157ddb-099c-4eb2-998d-fadde568cc53" />


---

## Uwagi

- API wykorzystuje uproszczony mechanizm autoryzacji – token przekazywany jest w nagłówku `Authorization` jako `Basic`, co nie jest standardowym podejściem (w praktyce stosuje się najczęściej Bearer token).
- Testy korzystają z istniejących danych (stałe ID zasobów), co może wpływać na ich stabilność w zależności od stanu środowiska.
- Projekt skupia się na pokazaniu sposobu testowania mechanizmów auth, a nie na pełnej walidacji bezpieczeństwa API.

---

## Wnioski

Testy pozwalają zweryfikować podstawowe scenariusze związane z autoryzacją oraz pokazują, jak API reaguje na brak lub błędne dane uwierzytelniające.  
Jednocześnie widoczne jest, że mechanizm autoryzacji w testowanym API jest uproszczony i nie w pełni odzwierciedla rozwiązania stosowane w systemach produkcyjnych.
