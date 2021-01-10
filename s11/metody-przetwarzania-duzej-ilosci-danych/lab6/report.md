# Metody przetwarzania dużych ilości danych

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
15.12.2020 18:55 | Data Mining | Adam Hyjek (234987)<br>Bartosz Rodziewicz (226105)

### Streszczenie laboratorium

### Problem 1
#### Stworzenie nowego projektu Analysis Services w SS BIDS

![](screenshots/01.png =400x0)  
_Stworzenie nowego projektu._

#### Stworzenie źródła danych

![](screenshots/02.png =400x0)  
_Stworzenie połączenia z bazą danych (różnica do instrukcji, serwer to nie localhost, a ITA)._

![](screenshots/03.png =500x0)  
_Wybór metody logowania._

#### Stworzenie widoku źródła danych

![](screenshots/05.png =500x0)  
_Wybór tabel do widoku źródła danych._

![](screenshots/06.png =500x0)  
_Nowy widok źródła danych._

#### Modyfikacja widoku źródła danych

![](screenshots/07.png =500x0)  
_Utworzenie nowego związku między tabelami._

### Problem 2
#### Stworzenie struktury eksploracji danych dla modelu Targeted Mailing

![](screenshots/08.png =500x0)  
_Wybór tabeli do eksploracji._

![](screenshots/09.png =500x0)  
_Wybór danych treningowych._

![](screenshots/10.png =500x0)  
_Podsumowanie tworzenia struktury eksploracji danych._

#### Przetwarzanie modelu ekstrakcji danych

![](screenshots/11.png =500x0)  
_Poprawny wynik przetwarzania._

<div class="page-break"></div>

#### Analiza modelu opartego o drzewa decyzyjne

![](screenshots/12.png =500x0)  
_Wygląd widoku analizy modelu._

#### Mapowanie kolumn

![](screenshots/13.png =500x0)  
_Mapowanie kolumn._

#### Macierz klasyfikacji

![](screenshots/14.png =500x0)  
_Wyniki macierzy klasyfikacji._

##### Jaki jest całkowity błąd predykcji drzewa decyzyjnego, a także jaka część osób odrzuci ofertę z kampanii?

| Wskaźnik | Działanie | Wynik |
| --- | --- | --- |
Całkowity błąd predykcji | (2734+2076)/(6618+2734+2076+7056) = 4810/18484 = ~0.26 | 26% |
Jaka część osób odrzuci ofertę | 2734/(2734+7056) = 1367/4895 = ~0.279 | 27.9%

#### Wykres przewidywanego zysku

![](screenshots/15.png =500x0)  
_Wybór parametrów wykresu._

![](screenshots/16.png =500x0)  
_Wykres dla indywidualnego kosztu równego 10._

##### Jak można zinterpretować otrzymany wykres?
Wykres mówi o tym jakiego zysku można się spodziewać wysyłając kampanie reklamową do wybranego procentu populacji uwzględniając całkowity koszt kampanii, koszt kampanii na osobę, możliwy zysk od osoby oraz prawdopodobieństwo, czy dana osoba zdecyduje się na zakupy.

<div class="page-break"></div>

##### Zbadaj kształt wykresu dla różnych wartości

![](screenshots/17.png =475x0)  
_Wykres dla indywidualnego kosztu równego 3._

![](screenshots/18.png =475x0)  
_Wykres dla indywidualnego kosztu równego 5._

![](screenshots/19.png =475x0)  
_Wykres dla indywidualnego kosztu równego 12._

Im wyższy koszt wykonania kampanii na osobę (przy takim samym potencjalnym zysku), tym bardziej się opłaca wysłać kampanie do mniejszej ilości, lepiej wyselekcjonowanych ludzi, przy których prawdopodobieństwo sukcesu jest większe.

##### Dlaczego przy ustawieniu Individual Cost powyżej wartości 15 wykres zysku nie posiada wartości dodatnich?

![](screenshots/20.png =475x0)  
_Wykres dla indywidualnego kosztu równego 16._

Wykres nie posiada wartości dodatnich, ponieważ potencjalny zysk z osoby, decydującej się na zakupy, jest niższy niż koszt wykonania kampanii.

#### Zmiany kolumn w modelu

![](screenshots/21.png =500x0)  
_Nowa wartość macierzy klasyfikacji._

##### Oblicz na nowo całkowity błąd predykcji i błąd dla kupna roweru. Czy otrzymane wyniki są lepsze czy gorsze od poprzednio uzyskanych?

| Wskaźnik | Działanie | Wynik |
| --- | --- | --- |
Całkowity błąd predykcji | (3414+2239)/(5938+3414+2239+6893) = 5653/18484 = ~0.3058 | 30.6% |
Jaka część osób odrzuci ofertę | 3414/(3414+6893) = 3414/10307 = ~0.33 | 33%

Wyniki są gorsze od poprzednich.

### Problem 2 – kontynuacja modułu 1
#### Algorytm naiwny Bayesowski

![](screenshots/23.png =500x0)  
_Nowy algorytm Bayesowski._

![](screenshots/24.png =500x0)  
_Wpływ poszczególnych atrybutów na wyniki._

![](screenshots/25.png =500x0)  
_Wpływ poszczególnych wartości atrybutów na wyniki._

<div class="page-break"></div>

##### Czy aktualnie stworzony model jest lepszy czy gorszy od drzew decyzyjnych?

![](screenshots/26.png =500x0)  
_Wynik macierzy klasyfikacji._

Algorytm jest gorszy.

##### Zmienić kolumny wejściowe dla tego modelu, czy można w ten sposób poprawić wyniki dla tego algorytmu?

![](screenshots/27.png =500x0)  
_Wynik macierzy klasyfikacji po dodaniu poprzednio wyłączonych atrybutów (imię, nazwisko, region)._

Wynik delikatnie się poprawił, jednak wciąż jest słabszy niż algorytm na podstawie drzew decyzyjnych.

#### Algorytm oparty o Sztuczne Sieci Neuronowe

![](screenshots/28.png =500x0)  
_Nowy algorytm SSN._

##### Jakie kolumny nie mogą być użyte przez sieć neuronową?
Wszystkie dostępne kolumny mogą być użyte poprzez sieć neuronową.

<div class="page-break"></div>

##### Porównaj opracowane modele. Które kolumny można zignorować?

![](screenshots/30.png =500x0)  
_Wynik macierzy klasyfikacji dla wszystkich argumentów._

Powyżej widać, że algorytm SSN jest trochę lepszy niż Bayesowski, jednak gorszy niż drzewa decyzyjne.

![](screenshots/29.png =500x0)  
_Analiza modelu._

Analiza modelu pokazuje, że duży wpływ na dane mają kolumny First and Last Name. Oczywistym jest, że te kolumny nie prezentują żadnych użytecznych informacji, więc można je wyłączyć.

![](screenshots/31.png =500x0)  
_Wynik macierzy klasyfikacji po wyłączeniu parametrów First and Last Name._

Powyżej widać, że wyniki delikatnie uległy poprawie, jednak nie jest to znaczący wynik.

##### Zmień kolumny wejściowe dla tego modelu, czy można w ten sposób poprawić wyniki dla tego algorytmu?

Kilkukrotna próba zmiany kolumn wejściowych nie spowodowała poprawy wyników.
