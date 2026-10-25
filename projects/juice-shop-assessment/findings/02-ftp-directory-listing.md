\# Public directory listing and sensitive files in /ftp



\## Severity

High



\## Klasyfikacja

\- CWE-548: Exposure of Information Through Directory Listing

\- OWASP Top 10: A05 Security Misconfiguration

\- OWASP WSTG: Review Old Backup and Unreferenced Files for Sensitive Information



\## Opis

Katalog /ftp jest dostępny bez uwierzytelnienia i zwraca listing plików.

Użytkownik niezalogowany może zobaczyć nazwy plików, ich rozmiary oraz daty modyfikacji.



\## Kroki reprodukcji

1\. Otwórz http://localhost:3000/robots.txt

2\. Zauważ wpis: Disallow: /ftp

3\. Otwórz http://localhost:3000/ftp

4\. Zaobserwuj listing plików



\## Dowód

HTTP/1.1 200 OK

Content-Type: text/html; charset=utf-8



Widoczne pliki:

\- acquisitions.md

\- announcement\_encrypted.md

\- coupons\_2013.md.bak

\- incident-support.kdbx

\- package.json.bak

\- package-lock.json.bak

\- suspicious\_errors.yml



\## Wpływ

Atakujący może odkryć wewnętrzne dokumenty, backupy konfiguracji, pliki

związane z bezpieczeństwem oraz potencjalne dane do dalszej eksploatacji.

Directory listing ułatwia mapowanie aplikacji i przygotowanie kolejnych ataków.



\## Rekomendacja

1\. Wyłączyć directory listing dla katalogów serwera.

2\. Usunąć backupy i pliki wewnętrzne z lokalizacji dostępnej przez WWW.

3\. Ograniczyć dostęp do /ftp uwierzytelnieniem i autoryzacją.

4\. Przenieść pliki wrażliwe poza katalog publiczny.

5\. Wdrożyć politykę retencji i usuwania plików tymczasowych.







\## Dodatkowa analiza plików



| Plik | Status | Wniosek |

|---|---:|---|

| /ftp/acquisitions.md | 200 OK | Publicznie dostępny dokument wewnętrzny |

| /ftp/package.json.bak | 403 Forbidden | Blokada rozszerzenia .bak |

| /ftp/suspicious\_errors.yml | 403 Forbidden | Blokada rozszerzenia .yml |

| /ftp/incident-support.kdbx | 200 OK | Publicznie dostępna baza KeePass |



\## Wniosek

Kontrola dostępu opiera się wyłącznie na rozszerzeniu pliku, a nie na

autoryzacji użytkownika ani lokalizacji pliku. Pliki .md i .kdbx są pobieralne,

choć mogą zawierać dane wewnętrzne lub wrażliwe.

