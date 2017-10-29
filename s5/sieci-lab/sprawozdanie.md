# Technologie sieciowe 2 - sprawozdanie
## Szacowanie wymaganej przepustowości łącza

#### Termin zajęć:
23.10.2017

#### Autorzy:
* Bartosz Rodziewicz, 226105
* Jan Potocki, <TODO: wstaw index>

### Treść zadania

W firmie <TODO: tu wstaw nazwę> pracuje 40 osób. Pracownicy przez 20% czasu przeglądają
strony WWW. Na 5 stacjach przez cały dzień pracy uruchomione jest radio internetowe,
na jednej stacji TV. Wszyscy pracownicy do komunikacji wykorzystują komunikatory
(wybrać jakie) oraz telefony IP lub softphony (wybrać) oraz pocztę elektroniczną.
2 razy w tygodniu odbywają się dwugodzinne wideokonferencje, w których uczestniczą
2 osoby (2 stacje). Administrator pobiera korzystając z FTP łatki, uaktualnienia,
nowe wersje oprogramowania. Administrator raz w tygodniu przesyła pełny
backup BD na zdalny serwer a codziennie backup 1/5 danych. Rozmiar BD to 14 GB.

### Krótki opis sposobów generowania ruchu
Ruch był sztucznie generowany przez nas poprzez wykonywanie typowych dzialań w
przykładowych aplikacjach. Każda aplikacja była przez nas używana przez 10 minut.
Po 10 minutach zapisywaliśmy całkowite dane pobrane (download) i wysłane (upload)
oraz ruch na sekundę. W trakcie testów obserwowaliśmy co jakiś czas zmienność
użycia w czasie.

### Analiza otrzymanych logów

#### Radio internetowe
* Testowana stacja: Radio Wrocław
* Całkowity ruch:
 * Download: <TODO: policzyc>
 * Upload: <TODO: policzyc>
* Ruch na sekundę:
 * Download: 141 kbit/s
 * Upload: 5 kbit/s
* Zmienność użycia w czasie:
 * Download: ±5 kbit/s
 * Upload: ±2 kbit/s

#### Przegladanie internetu
* Testowane strony:
 * Onet
 * WP
 * Radio Wrocław
* Całkowity ruch:
 * Download: <TODO: policzyc>
 * Upload: <TODO: policzyc>
* Ruch na sekundę:
 * Download: 129 kbit/s
 * Upload: 9 kbit/s
* Zmienność użycia w czasie:
 * Download: mocno zmienne w czasie
 * Upload: mocno zmienne w czasie

#### Telewizja internetowa
* Testowana usługa: Youtube
* Całkowity ruch:
 * Download: <TODO: policzyc 771.7 MB>
 * Upload: <TODO: policzyc>
* Ruch na sekundę:
 * Download: 1333 kbit/s
 * Upload: 74 kbit/s
* Zmienność użycia w czasie
 * Download: ±100 kbit/s
 * Upload: ±10 kbit/s

#### Komunikatory
* Testowana aplikacja: Telegram

#### Telefony IP
<TODO: cos wymyslic>

#### Poczta elektroniczna

#### Rozmowy audio
* Testowana aplikacja: Skype

#### Rozmowy wideo
* Testowana aplikacja: Skype

#### Pobieranie po FTP
* Całkowity ruch:
 * Download: <TODO: policzyc>
 * Upload: <TODO: policzyc>
* Ruch na sekundę:
 * Download: 3198 kbit/s
 * Upload: 70 kbit/s
* Zmienność użycia w czasie:
 * Download: niewielka
 * Upload: niewielka

#### Wysyłanie po FTP
 * Całkowity ruch:
  * Download: <TODO: policzyc>
  * Upload: <TODO: policzyc>
 * Ruch na sekundę:
  * Download: 76 kbit/s
  * Upload: 2729 kbit/s
 * Zmienność użycia w czasie:
  * Download: niewielka
  * Upload: niewielka

*Download w trakcie pobierania po FTP i upload w trakcie wysyłania po FTP wykorzystuje całą dostępną przepustowość.*

### Wyliczenia pasma i ruchu związanego z poszczególnymi usługami

### Wyliczenie przepustowości łącza do Internetu dla rozważanej firmy

### Wybór i opis łącza do Internetu dla rozważanej firmy

### Wnioski

### Pytania:

#### Które usługi mają profil ruchu symetryczny, a które asymetryczny?

#### W jakich przypadkach w firmie niezbędne jest symetryczne łącze do Internetu?

#### Co to jest CIR?

#### Czy najważniejszym parametrem dla usługi sieciowej jest pasmo (przepustowość)?

#### Jakie usługi sieciowe wymagają także zapewnienia innych parametrów sieci (wymienić te parametry)?

#### Czy cena za łącza Internetowe rośnie liniowo wraz z przepustowością tego łącza?
