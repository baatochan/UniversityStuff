# Rozległe sieci komputerowe

## Sprawozdanie z laboratorium

Data				| Tytuł zajęć												| Uczestnicy				
--------------------|-----------------------------------------------------------|---------------------------
05.03.2018 07:30	| Konfiguracja VLAN, łącza trunk i zabezpieczeń sieci VLAN	| Iwo Bujkiewicz (226203)<br />Bartosz Rodziewicz (226105)<br />Dominik Szymon Cecotka

### Wyniki realizacji zadań

#### Część 1. Budowa sieci i konfiguracja podstawowych ustawień urządzeń

* **Czy ping z PC-A do PC-B zakończył się sukcesem?**
	Tak
* **Czy ping z PC-A do PC-C zakończył się sukcesem?**
	Nie
* **Czy ping z PC-A od S1 zakończył się sukcesem?**
	Nie
* **Czy ping z PC-B do PC-C zakończył się sukcesem?**
	Nie
* **Czy ping z PC-B do S2 zakończył się sukcesem?**
	Nie
* **Czy ping z PC-C do S2 zakończył się sukcesem?**
	Tak
* **Czy ping z S1 do S2 zakończył się sukcesem?**
	Tak
* **Jeśli którakolwiek odpowiedź brzmi "nie", napisz, dlaczego pingi się nie powiodły.**
	
	Interfejsy sieciowe urządzeń znajdowały się w dwóch podsieciach - `192.168.10.0/24` (PC-A, PC-B) oraz `192.168.99.0/24` (PC-C, S1, S2). W sieci nie było przełącznika warstwy 3, więc niemożliwe było pingowanie urządzeń z innej podsieci.

#### Część 2. Tworzenie sieci VLAN i przypisywanie do nich portów

##### Krok 1.

* **Jaki jest domyślny VLAN?**
	
	VLAN 1
	
* **Jakie porty są dołączone do domyślnej sieci VLAN?**
	
	Wszystkie interfejsy sieciowe przełącznika

##### Krok 2.

* **Jaki jest status VLAN 99? Dlaczego?**
	
	Up, ponieważ wirtualny interfejs sieciowy przełącznika odpowiadający VLAN 99 otrzymał adres IP i został tym samym włączony.
	
* **Czy ping z PC-A do PC-B zakończył się sukcesem? Dlaczego?**
	
	Nie, ponieważ nie istniała trasa wartstwy 2 pomiędzy PC-A i PC-B, która przebiegałaby wewnątrz jednego VLAN lub jednego VLAN i połączenia typu trunk.
	
* **Czy ping z S1 do S2 zakończył się sukcesem? Dlaczego?**
	
	Tak, ponieważ interfejsy przełączników połączone między sobą były przypisane do jednego VLAN i jednej podsieci IP.

#### Część 3. Zachowanie konfiguracji portów w sieci VLAN i bazy danych sieci VLAN.

##### Krok 2.

* **Do którego VLAN przyporządkowany jest teraz interfejs F0/24?**
	
	VLAN 1

##### Krok 3.

* **Jaka jest domyślna nazwa sieci VLAN 30?**
	
	VLAN0030
	
* **F0/24 był przypisany do sieci VLAN 30. Do czego przypisany jest interfejs F0/24 po skasowaniu VLAN 30? Co się stało z ruchem kierowanym do hosta przypiętego do interfejsu F0/24?**
	
	Po skasowaniu VLAN 30 interfejs nie był przypisany do żadnego VLAN. Nie było ruchu do hosta na F0/24 (żaden host nie był podłączony do F0/24).
	
* **Wydaj komendę `show vlan brief` w celu określenia, do jakiej sieci VLAN przyporządkowany jest interfejs F0/24. Do jakiej sieci VLAN przyporządkowany jest interfejs F0/24?**
	
	VLAN 1
	
* **Dlaczego należy ponownie przyporządkować interfejs do innego VLAN przed usunięciem VLAN z bazy danych?**
	
	Aby interfejs nie pozostał nieprzypisany do żadnego VLAN a tym samym bezużyteczny.

#### Część 4. Konfiguracja 802.1q trunk pomiędzy przełącznikami

##### Krok 1.

* **Czy ping z PC-A do PC-B zakończył się sukcesem?**
	Tak
* **Czy ping z PC-A do PC-C zakończył się sukcesem?**
	Nie
* **Czy ping z PC-A do S1 zakończył się sukcesem?**
	Nie
* **Czy ping z PC-B do PC-C zakończył się sukcesem?**
	Nie
* **Czy ping z PC-B do S2 zakończył się sukcesem?**
	Nie
* **Czy ping z PC-C do S2 zakończył się sukcesem?**
	Nie
* **Jeśli którakolwiek odpowiedź brzmi "nie", wyjaśnij, dlaczego.**
	
	Ponieważ gdy w sieci nie ma przełącznika warstwy 3, to nawet w przypadku istnienia połączenia trunk przesyłać dane między sobą mogą tylko urządzenia w tym samym VLAN i tej samej podsieci IP.

##### Krok 2.

* **Dlaczego warto ręcznie skonfigurować interfejs w trybie trunk zamiast za pomocą DTP?**
	
	Ponieważ w ten sposób administrator ma pewność, że trunk jest faktycznie włączony na danym interfejsie przełącznika.

#### Część 5. Implementacja zabezpieczeń sieci VLAN

##### Krok 2.

* **Jaki jest natywny VLAN dla przełącznika S1 i S2 na interfejsie F0/1?**
	
	VLAN 1
	
* **Poczekaj kilka sekund. Na konsoli przełącznika S1 powinny pojawiać się komunikaty o błędzie. Co oznacza wiadomość `%CDP-4-NATIVE_VLAN_MISMATCH:`?**
	
	Natywny VLAN ustawiony dla interfejsu trunk przełącznika jest różny od natywnego VLAN dla interfejsu przełącznika po drugiej stronie łącza.

###### Krok 3.

* **Z linii komend komputera PC-A (wywołaj CMD z menu) wykonaj komendę ping na adres IP sieci zarządzania na przełączniku S1. Czy test łączności zakończył się sukcesem? Dlaczego?**
	
	Nie, ponieważ interfejs sieciowy PC-A znajduje się w innej podsieci IP, a przeznaczony dla niego interfejs przełącznika przypisany jest do innego VLAN, niż wirtualny interfejs sieciowy S1.
	
* **Z przełącznika S1 wykonaj komendę ping na adres zarządzania na przełączniku S2. Czy test łączności zakończył się sukcesem? Dlaczego?**
	
	Tak, ponieważ wirtualne interfejsy sieciowe S1 i S2 są przypisane do tego samego VLAN oraz tej samej podsieci IP.
	
* **Z linii komend komputera PC-B wykonaj komendę ping na adres zarządzający na przełącznikach S1 i S2 i adres IP PC-A i PC-C. Czy test łączności zakończył się sukcesem? Dlaczego?**
	
	Test łączności do S1, S2 oraz PC-C nie powiódł się, ponieważ urządzenia te znajdują się w innym VLAN i innej podsieci IP. Test łączności do PC-A powiódł się.
	
* **Z linii komend komputera PC-C wykonaj komendę ping na adres zarządzający na przełącznikach S1 i S2. Czy test łączności zakończył się sukcesem? Dlaczego?**
	
	Tak, ponieważ znajduje się w tym samym VLAN i podsieci IP, co wirtualne interfejsy S1 i S2.

##### Krok 5.

* **Jaki jest rezultat?**
	
	* Nie będzie można podłączyć niepowołanego łącza trunk do wolnych portów przełącznika;
	* Nie będzie można przesyłać po skonfigurowanym łączu trunk ramek wewnątrz VLAN innych, niż skonfigurowane;
	* Nie będzie można podłączyć niepowołanych urządzeń do VLAN użytkowych oraz domyślnego.

#### Część 6. Kasowanie bazy danych VLAN.

##### Krok 2.

* **Jakie komendy należy jeszcze wydać, aby zainicjować przełącznik z jego ustawieniami fabrycznymi?**
	
	`# erase startup-config`
	
	`# reload`

### Odpowiedzi na pytania

1. **Jakie, jeśli w ogóle, występują problemy z bezpieczeństwem na przełącznikach CISCO dla ustawień domyślnych?**
	
	* Możliwość podłączania nowych, niekoniecznie autoryzowanych urądzeń do wolnych portów przełącznika;
	
1. **Co jest potrzebne, aby umożliwić komunikację pomiędzy hostami z VLAN 10 z hostami należącymi do VLAN 20?**
	
	Przełącznik warstwy 3
	
1. **Jakie są główne korzyści, które organizacja może uzyskać w wyniku efektywnego wykorzystania sieci VLAN?**
	
	Minimalizacja ilości wymaganego sprzętu przy rozdzielaniu ruchu sieciowego o różnym przeznaczeniu
