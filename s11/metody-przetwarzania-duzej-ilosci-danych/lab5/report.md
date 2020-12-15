# Metody przetwarzania dużych ilości danych

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
01.12.2020 18:55 | Zaawansowana analiza danych | Adam Hyjek (234987)<br>Bartosz Rodziewicz (226105)

### Streszczenie laboratorium
Instrukcja laboratoryjna nr 5 przedstawia metodę definiowania nowego wymiaru z wykorzystaniem tabeli pośredniej oraz metodę definiowania wymiaru wykorzystując tabelę faktów. Przedstawiony tam jest również proces tworzenia tłumaczenia (translacji) na inny język opisów kostki danych oraz wymiarów. Opisana również jest metoda definiowania własnych partycji w kostkach danych oraz tworzenia własnych agregacji danych w tych partycjach. Wszystkie te zadania (podstawowe) są przedstawione poniżej w tym sprawozdaniu.

### Różne rodzaje wymiarów
#### Definiowanie wymiaru połączonego przez tabelę pośrednią

![](screenshots/01.png =500x0)  
_Dodanie brakujących tabeli Product Category i Product Subcategory._

![](screenshots/02.png =400x0)  
_Tworzenie nowego wymiaru Product Subcategory._

![](screenshots/04.png)  
_Dodanie nowego wymiaru do measure grupy i ustawienie jego parametrów._

#### Tworzenie wymiaru z tabeli faktów

![](screenshots/05.png)  
_Dodanie nowego wyliczania._

![](screenshots/06.png =349x0)
![](screenshots/07.png =349x0)  
_Tworzenie nowego wymiaru._

![](screenshots/08.png)  
_Dodanie atrybutu z kolumny oraz zmiana parametru._

![](screenshots/09.png)  
_Dodanie wymiaru do measure grupy._

### Definiowanie translacji
#### Definiowanie nowej translacji

![](screenshots/10.png)  
_Dodanie nowej translacji na j. polski._

<div class="page-break"></div>

#### Definiowanie nazw dla nowej translacji

![](screenshots/11.png)  
_Uzupełnienie tłumaczeń kostki dla tłumaczenia na j. polski (mamy nadzieję, że nie będzie oceniana jakość tłumaczenia)._

<div class="page-break"></div>

#### Wypełnianie translacji dla wymiaru

![](screenshots/12.png =650x0)  
_Uzupełnienie tłumaczeń wymiaru Time dla tłumaczenia na j. polski (mamy nadzieję, że nie będzie oceniana jakość tłumaczenia)._

#### Translacja dla wymiaru Product

![](screenshots/13.png =650x0)  
_Uzupełnienie tłumaczeń wymiaru Produkt dla tłumaczenia na j. polski._

#### Weryfikacja translacji

![](screenshots/14.png)  
_Polskie nazwy widoczne w zakładce Browser._

### Partycje w kostkach danych
#### Sprawdzanie dostępnych partycji dla każdej grupy agregacji

![](screenshots/15.png)  
_Domyślne partycje przypisane do grup pomiarów. Grupa Internet Sales posiada tylko jedną partycję._

<div class="page-break"></div>

#### Utworzenie nowych partycji

![](screenshots/16.png =350x0)  
_Do utworzenia ręcznych partycji konieczne jest usunięcie domyślnej._

![](screenshots/17.png =350x0)  
_Tworzenie nowej partycji - dane źródła._

![](screenshots/18.png =350x0)  
_Tworzenie nowej partycji - zapytanie ograniczające._

![](screenshots/19.png)  
_Tworzenie nowej partycji - ustalenie poprawnej nazwy partycji._

#### Zadanie utworzenia partycji

![](screenshots/20.png =230x0)
![](screenshots/21.png =230x0)
![](screenshots/22.png =230x0)  
_Tworzenie 3 kolejnych partycji._

![](screenshots/23.png)  
_Utworzone 4 partycje._

<div class="page-break"></div>

#### Zmiana agregacji dla partycji

![](screenshots/24.png =400x0)  
_Zmiana trybu agregacji danych._

W programie dostępne są następujące presety:
* MOLAP
	* dane measure grup oraz agregacji przechowywane są w formacie wielowymiarowym
	* powiadomienia są pokazywane, gdy dane ulegną zmianie
	* wczytywanie nowych danych jest wykonywane ręcznie
* Scheduled MOLAP
	* różni się tym od MOLAP, że wczytywanie nowych danych jest wykonywane automatycznie co 24h
* Automatic MOLAP
	* różni się tym od MOLAP, że powiadomienia o zmianie danych wyzwalają automatyczne wczytywanie danych, co powoduje, że nowe dane są wczytywane bez opóźnień
* Medium-latency MOLAP
	* różni się tym od Automatic MOLAP, że dane nie są wczytywane bez opóźnienia, a z opóźnieniem maksymalnie kilku godzinnym.
* Low-latency MOLAP
	* różni się tym od Automatic MOLAP, że dane nie są wczytywane bez opóźnienia, a z opóźnieniem maksymalnie 30 minutowym.
* Real-time HOLAP
	* różni się tym od MOLAP, że dane measure grup przechowywane są w formacie relacyjnym, natomiast agregacje w formacie wielowymiarowym; dane zawsze oddają stan rzeczywisty
* Real-time ROLAP
	* różni się tym od Real-time HOLAP, że i measure grupy, jak i agregacje są przechowywane w formacie relacyjnym

Zmiana z MOLAP na Scheduled MOLAP powoduje, że hurtownia danych będzie automatycznie co 24h aktualizowała swoje dane.

![](screenshots/25.png =400x0)  
_Szczegółowe ustawienia Scheduled MOLAP._

![](screenshots/26.png =400x0)  
_Nieskonfigurowane szczegółowe ustawienia Medium-latency MOLAP._

![](screenshots/27.png)  
_Konfiguracja zapytania powiadamiającego o zmianie, po zapisaniu zapytania zapytanie rozwinęło `*`._

#### Konfiguracja opcji agregacji

![](screenshots/28.png =500x0)  
_Konfiguracja agregacji - liczność poszczególnych wymiarów._

![](screenshots/29.png =500x0)  
_Konfiguracja agregacji - ustawienie szacowanej liczności poszczególnych wymiarów._

#### Strojenie agregacji

![](screenshots/30.png)  
_Konfiguracja agregacji - domyślne szacunki strojenia agregacji dla 50% zysku wydajności. Zostało wykonane 28 agregacji._

![](screenshots/31.png)  
_Konfiguracja agregacji - domyślne szacunki strojenia agregacji dla 30% zysku wydajności. Również zostało wykonane 28 agregacji._

![](screenshots/32.png)  
_Konfiguracja agregacji - szacunki strojenia agregacji po zwiększeniu ilości Produktów. Zostało wykonane 21 agregacji._

#### Przegląd agregacji utworzonych w zbiorze `AdventureWorks.partition`

![](screenshots/33.png)  
_Definicja agregacji w kodzie źródłowym._

#### Zmiana agregacji dla poziomów

![](screenshots/34.png)  
_Zmiana metody agregacji dla atrybutu Color wymiaru Product._

![](screenshots/35.png)  
_Przy tworzeniu nowej agregacji atrybut Color automatycznie ustawiony jest na full._
