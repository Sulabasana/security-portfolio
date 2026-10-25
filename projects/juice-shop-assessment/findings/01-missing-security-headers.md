\# Missing security headers



\## Podsumowanie

Aplikacja nie ustawia nagłówka Content-Security-Policy oraz Referrer-Policy.

Pozostałe nagłówki bezpieczeństwa są częściowo skonfigurowane.



\## Severity

Low / Medium — zależnie od kontekstu produkcyjnego.



\## Dowód

curl.exe -I http://localhost:3000



Odpowiedź nie zawierała:

\- Content-Security-Policy

\- Referrer-Policy

\- Permissions-Policy z restrykcyjną konfiguracją



\## Wpływ

Brak CSP zwiększa ryzyko skutecznego XSS oraz ładowania niepożądanych zasobów.

Brak Referrer-Policy może powodować wyciek informacji o źródle żądania.



\## Rekomendacja

Dodać restrykcyjny nagłówek CSP, np. w pierwszej wersji:



Content-Security-Policy: default-src 'self'; object-src 'none'; frame-ancestors 'none'



Dodać:



Referrer-Policy: strict-origin-when-cross-origin



\## Status

Open

