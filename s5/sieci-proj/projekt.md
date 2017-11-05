# Technologie Sieciowe 2 - Projekt
*Krzysztof Agieńczuk, <TODO: podaj numer indexu>*  
*Bartosz Rodziewicz, 226105*

### Terminy oddania etapów:
* Etap 1 - 07.11.2017
* Etap 2 - 05.12.2017
* Etap 3 - 16.01.2018

## Wstęp
Projekt polega na zaprojektowaniu lokalnej sieci komputerowej dla dużego przedsiębiorstwa, w naszym przypadku jest to **Agencja Turystyczna**. W budynkach należących do przedsiębiorstwa zostało zainstalowane okablowanie strukturalne (kat. 6) wraz z niezbędnymi szafami teleinformatycznymi. Przedsiębiorstwo posiada także wszystkie urządzenia końcowe (serwery, drukarki, komputery, kamery IP, itp.), które należy podłączyć do sieci. Zakres projektu obejmuje opracowanie projektu logicznego sieci, projektu VLAN, wybór technologii sieciowej i urządzeń sieciowych oraz podstawową konfigurację urządzeń, tak aby zapewnić prawidłowe i niezawodne działanie sieci.

## Inwentaryzacja zasobów: sprzętu, aplikacji, zasobów ludzkich
### Inwentaryzacja sprzętu
| Liczba komputerów pracowników | Bud. 1 p. 1 | Bud. 1 p. 2 | Bud. 1 p. 3 | Bud. 1 p. 4 | Bud. 2 p. 1 |
| :-: | :-: | :-: | :-: | :-: | :-: |
| Sprzedawcy | 30 | 22 | 43 | 58 | 66 |
| Konsultanci | 53 | 24 | 75 | 9 | 10 |
| Księgowość | 37 | 46 | 63 | 57 | 57 |
| **Liczba drukarek** |
| | 2 |	3 |	1 |	1 |	3 |
| **Liczba punktów dostępowych Wi-Fi** |
| | 0	| 2	| 2 |	0 |	0 |
| **Liczba urządzeń bezprzewodowych** |
| | 0	| 8 |	9 |	0 |	0 |

#### Serwery lokalne
Firma posiada dwa serwery lokalne

#### Punkty dystrybucyjne
| Oznaczenie |	Lokalizacja |	Podłączone punkty abonenckie |
| :-: | :-: | :-: |
| MDF	| Bud. 1, p. 1	| Bud. 1, p. 1 |
| IDF1	| Bud. 1, p. 4	| Bud. 1, p. 2, 3, 4 |
| IDF2 |	Bud. 2, p. 1	| Bud. 2 |

#### Połączenie między budynkami
Firma znajduje się w dwóch budynkach, których odległość od siebie wynosi 274m. Budynki połączone są łączem optycznym wielomodowym.


### Inwentaryzacja aplikacji
Pracownicy będą korzystać z następujących aplikacji:
* Przeglądarka
* Wideokonferencja
* VoIP
* Klient FTP
* Komunikator
* Praca w chmurze
* Poczta

### Inwentaryzacja zasobów ludzkich

| Grupa robocza | Bud. 1 p. 1 | Bud. 1 p. 2 | Bud. 1 p. 3 | Bud. 1 p. 4 | Bud. 2 p. 1 | Razem |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Sprzedawcy | 30 | 22 | 43 | 58 | 66 | **219** |
| Konsultanci | 53 | 24 | 75 | 9 | 10 | **171** |
| Księgowość | 37 | 46 | 63 | 57 | 57 | **260** |


## Analiza potrzeb użytkowników – wymagania zamawiającego
### Wymagania dot. przepływów pomiędzy pracownikami a serwerami lokalnymi
Transfer do serwerów lokalnych i drukarek (down \ up) [kb/s]

| Grupa rob. / Serwer |	Serwer1 |	Serwer2 |	Drukarka |
| :-: | :-: | :-: | :-: |
| Sprzedawcy |	500\600 |	0\0 |	10\190 |
| Konsultanci |	0\0 |	0\0 |	10\140 |
| Księgowość |	250\900 |	0\0 |	10\120 |
| Wi-Fi |	200\200 |	0\0 |	10\170 |

### Prognozowany ruch do Internetu z posiadanych przez firmę serwerów internetowych
Transfer do\z Internetu na jedną sesję (internautę) [kb/s]

| Serwery internetowe	| Do Internetu	| Z Internetu	| Liczba jednoczesnych sesji |
| :-: | :-: | :-: | :-: |
| Serwer WWW	| 140	| 30	| 44 |
| Serwer FTP	| 380	| 60	| 15 |

### Wymagania dot. przepływów generowanych przez aplikacje użytkownika z\do internetu
Transfer z/do Internetu (down \ up) [kb/s]

| Grupa rob./Aplikacja	| Przeglądarka	|	Wideokonferencja	|	VoIP	|	Klient FTP	|	Komunikator	|	Praca w chmurze	|	Poczta	|
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Sprzedawcy	|	0\0	|	40\40	|	20\20	|	45\18	|	15\15	|	27\44	|	19\14	|
| Konsultanci	|	0\0	|	40\40	|	20\20	|	51\17	|	15\15	|	25\46	|	23\15	|
| Księgowość	|	0\0	|	40\40	|	20\20	|	0\0	|	15\15	|	0\0	|	22\30	|
| Wi-Fi	|	56\10	|	40\40	|	20\20	|	0\0	|	0\0	|	60\26	|	24\29	|
