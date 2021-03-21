# Lokalne sieci komputerowe

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
17.03.2021 9:15 | Agregacja łączy | Bartosz Rodziewicz (226105)

### Konfiguracja EtherChannel
#### Podsumowanie konfiguracji EtherChannel
![Konfiguracja etherchannel](screenshots/01.png)

#### Do przemyślenia
* Co może przeszkadzać w tworzeniu się kanałów EtherChannel?  
	Błędy w konfiguracji, takie jak ustawienie portu jako trunk po jednej stronie zostawiając port w trybie access po drugiej, różne protokoły agregacji po obu stronach, czy różne prędkości portów.

### Rozwiązywanie problemów z EtherChannel
#### Zauważone problemy
##### Problemy S1
* Porty f0/1-2 skonfigurowane jako LACP
* Porty Po2 nie skonfigurowane jako porty trunk
##### Problemy S2
* Porty f0/3-4 nie były włączone
* Vlan10 nie znajdował się na liście dozwolonych vlanów Po1
##### Problemy S3
* Porty f0/3-4 były skonfigurowane jako Po3, a nie Po2
* Porty f0/1-2 były zupełnie nie skonfigurowane (nie włączone, nie dodane do Po3, nie ustawione jako trunk, brak natywnego vlanu)
* Porty Po2 nie miały ustawionego natywnego vlanu
