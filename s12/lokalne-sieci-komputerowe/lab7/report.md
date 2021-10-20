# Lokalne sieci komputerowe

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
28.04.2021 9:15 | Zaawansowana konfiguracja protokołu EIGRP | Bartosz Rodziewicz (226105)

### Zaawansowana konfiguracja protokołu EIGRP dla funkcji IPv4

#### Do przemyślenia
* Jakie są zalety tras podsumowanych?  
	Trasy podsumowane mogą służyć do ograniczenia liczby ogłoszeń routingu i rozmiaru tablic routingu. Zaletą tras podsumowanych jest to, że zmniejszają liczbę wpisów w tabeli tras, co zmniejsza obciążenie routera i obciążenie sieci oraz ogranicza liczbę ogłoszeń routingu.
* Podczas ustawiania liczników EIGRP, dlaczego tak ważne jest, aby wartość czasu wstrzymania była równa lub większa od przedziału czasowego pakietów hello?  
	Inne ustawienie może powodować poważne problemy ze stabilnością sieci. Jeśli czas wstrzymania jest krótszy niż czas pakietu hello, będziemy często obserwować utratę statusu sąsiada, powodując niestabilność.
* Dlaczego tak ważna jest konfiguracja uwierzytelniania dla EIGRP?  
	Dodanie uwierzytelniania do wiadomości EIGRP routerów gwarantuje, że routery będą akceptować wiadomości routingu tylko z innych routerów, które znają ten sam klucz wstępny. Bez skonfigurowanego uwierzytelniania, jeśli ktoś wprowadzi do sieci inny router z innymi lub sprzecznymi informacjami o trasie, tablice routingu na routerach mogą zostać uszkodzone i może nastąpić atak typu DDoS. Dlatego dodanie uwierzytelnienia do wiadomości EIGRP przesyłanych między routerami zapobiega celowemu lub przypadkowemu dodaniu innego routera do sieci i spowodowaniu problemu.

### Rozwiązywanie problemów związanych z podstawowym protokołem EIGRP dla IPv4 i IPv6

#### Do przemyślenia
* Dlaczego rozwiązywałbyś problemy dotyczące EIGRP dla IPv4 oraz EIGRP dla IPv6 oddzielnie?  
	Protokoły EIGRP dla IPv4 i EIGRP dla IPv6 nie współużytkują informacji o routingu, a ich konfiguracja jest całkowicie niezależna. Rozwiązywanie problemów powinno być wykonywane niezależnie dla każdego protokołu.
