\# OWASP Juice Shop — Security Assessment



\## Cel

Kontrolowany test bezpieczeństwa lokalnie uruchomionej aplikacji OWASP Juice Shop.



\## Zakres

\- Aplikacja webowa

\- API

\- Autoryzacja i uwierzytelnianie

\- Podatności z OWASP Top 10



\## Narzędzia

\- Docker

\- Przeglądarka

\- Burp Suite Community / OWASP ZAP

\- Nmap

\- curl / Postman



\## Status

\- \[x] Utworzenie dokumentacji

\- \[ ] Uruchomienie aplikacji

\- \[ ] Reconnaissance

\- \[ ] Testy logowania i autoryzacji

\- \[ ] Testy API

\- \[ ] Raport końcowy



\## Cel testu

Ocena podstawowego poziomu bezpieczeństwa lokalnie uruchomionej aplikacji OWASP Juice Shop.



\## Metodologia

Testowanie według OWASP Web Security Testing Guide (WSTG):

recon, identyfikacja punktów wejścia, testy autoryzacji, API i podatności webowych.



\## Znalezisko 2 — Poison Null Byte bypass



\- Severity: High

\- Klasyfikacja: CWE-436, OWASP A05 Security Misconfiguration

\- Status: Open



Filtr rozszerzeń w /ftp można obejść przez dodanie zakodowanego null byte

(%2500) oraz dozwolonego rozszerzenia .md. Pliki package.json.bak oraz

suspicious\_errors.yml, wcześniej blokowane odpowiedzią 403, stają się dostępne.



Rekomendacja: nie opierać autoryzacji na rozszerzeniu pliku, wdrożyć kontrolę

dostępu dla całego katalogu oraz usuwać backupy z lokalizacji publicznej.

