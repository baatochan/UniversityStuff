## Czytniki optyczne

### SPEAKER NOTES:
najstarsze, powstaly w latach 70, wyniki badan dla FBI  
efektywnie dzialja podobnie jak aparaty fotograficzne i wykonuja zdjecie odciska palca  
wykorzystuja zrodlo swiatla, pryzmat oraz matryce CCD (jak w aparatach cyfrowych)  
najproszte do oszukania z wszystkich, wydruk zdjecia linii papiarnych  

## Budowa czytnika optycznego

### SPEAKER NOTES:
The scanning process starts when you place your finger on a glass plate, and a CCD camera takes a picture. The scanner has its own light source, typically an array of light-emitting diodes, to illuminate the ridges of the finger. The CCD system actually generates an inverted image of the finger, with darker areas representing more reflected light (the ridges of the finger) and lighter areas representing less reflected light (the valleys between the ridges).

## Zmniejszony czytnik optyczny

### SPEAKER NOTES:
Ciekawostka: 2016, Synaptic, minimalizacja, pierwszy smartfon sensor optyczny pod ekranem  
tylko wyswietlace OLED  

---

## Czytniki pojemnościowe

### SPEAKER NOTES:
najpopularniejsze, zwykli uzytkownicy  
przewodzenie pradu przez skore  
matryca malych kondensatorow, wzgorza na palcu zaburzaja pojemnosci  

These sensors too scan the ridges and valleys on fingerprints. However, in this case, electric current is used to collect data instead of light. An array of capacitors are placed below the scanning surface to collect fingerprint detail. When a fingertip is placed on the scanning surface the charge stored on the capacitor changes. This difference in charge is tracked by an op-amp integrator circuit which is further recorded by an analogue-to-digital converter.

## Czytniki ultradźwiękowe

### SPEAKER NOTES:
stosunkowo nowe

Ich zasada działania opiera się na zjawisku dyfrakcji, odbicia oraz rozproszenia fali dźwiękowej. Gdy przykładamy do takiego czytnika palec, zaczyna on generować niesłyszalne dla naszych uszu dźwięki. Sposób zachowania się fal dźwiękowych w miejscach styku grzbietów opuszki z czytnikiem jest zupełnie inny niż w dolinach (w których jest powietrze). Pozwala to wygenerować dokładny obraz linii papilarnych palca.

potrafia generowac model 3d  
bardzo bezpieczna metoda  
czytniki pod szklo, plastik metal  
popularyzacja czytnikow pod ekranem (dziala z LCD)  
wolniejsze  

## Inne rodzaje czytników
### SPEAKER NOTES:
### termiczne
technologia podobna jak w kamerach na podczerwien  
dokladna, jednak dosc problematycnza metoda  
dotykajacy palec podgrzewa powierznie czytnika powodujac bardzo szybkie zamazanie odczytywanego obrazu (0.1s)  
wymaga aby temp otoczeia byla inna niz temp palca  

#### nacisku
wykorzystuja powierzchnie reagujaca na nacisk, wiele modeli odczytywalo nacisk 0-1, obrazy czarnobiale bez odcieni szarosci

#### radiowe
fale o niskiej czestotliosci, macierz detekcji wiele malych anten  
zaleta - niska podatnosc na uszkodzenia naskorka na palcu  

---

## Podział czytników ze względu na budowę

### SPEAKER NOTES:
wsyztskie na zdjeciach - statyczne  
wiekszosc nowych to statyczne  
sa bardziej dokladne  

przesuwne sa odpowiednikiem jednwymairowej matrycy czujnikow  
tansze w budowie  
glownie pojemnosciowe, wczesniej rowzniez optyczne  
zmienna predkosc przesuwania palca moze powodowac deformacje wynikowego obrazu  

---

## Metoda oparta na analizie minucji

### SPEAKER NOTES:
analiza obrazkow odczytow  pod wzgledem minuncji, porownanie ze wzorecem  
wzorzec, najczesciej kilka, wektor punktow  
punkty - wzgledna pozycja, typ (roznie), kierunek  
najczesciej sotosowana metoda, wiekszosc urzadzen konumenckich  

## Wizualizacja

### SPEAKER NOTES:
zjdecie wizualizacje punktow, po dzialanie algorytmu, naniesiona na obr wejsciowe, brak typu

## Polaczona wizualizacja

### SPEAKER NOTES:
naniesione obrazy z poprzedniego slajdu, blekitny idealne dopasowanie, alg wprowadza margines bledu i ilosc wymaganych

mozna tez wpomneic o tym jak dziala caly proces - zaprograowanie urzadzenia, popbranie odczytu(ow), wyostrzenie i odszumienei obrazow, przpeusczenie przez algorytm, zpaisanie (kilku) wzorow  
pobraniem, to samo z obrazkiem, algoerytm, porownanie, czy psauje do ktoregos  
wprowadzone marginesy bledow i wystarczajaca liczbe pasujacych robi mozliwosc stworzenia master palca, oddblokuje wiekszosc urzadzen, badania New York University Tandon School of Engineering and Michigan State University College of Engineering  
