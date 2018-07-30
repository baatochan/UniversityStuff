# Rozległe sieci komputerowe

## Sprawozdanie z laboratorium

Data				| Tytuł zajęć												| Uczestnicy				
--------------------|-----------------------------------------------------------|---------------------------
19.03.2018 07:30	| Konfiguracja routingu między sieciami VLAN				| Iwo Bujkiewicz (226203)<br />Bartosz Rodziewicz (226105)<br />Dominik Szymon Cecotka

### Wyniki realizacji zadań - instrukcja 5.1.

#### Część 3. Weryfikacja łącza trunkowego, sieci VLAN, routing i łączności

##### Krok 1.

* **Na R1, wydaj komendę `show ip route`. Jakie ścieżki zostały wylistowane na R1?**

    ```
    Gateway of last resort is not set

          192.168.10.0/24 is variably subnetted, 2 subnets, 2 masks
    C        192.168.10.0/24 is directly connected, GigabitEthernet0/1
    L        192.168.10.1/32 is directly connected, GigabitEthernet0/1
          192.168.20.0/24 is variably subnetted, 2 subnets, 2 masks
    C        192.168.20.0/24 is directly connected, GigabitEthernet0/0
    L        192.168.20.1/32 is directly connected, GigabitEthernet0/0
    ```

* **Wydaj komendę show interface trunk na S1 i S2. Czy port F0/1 na obu przełącznikach został ustawiony trunk?**
    Tak

* **Dlaczego F0/1 nie znajduje się na liście aktywnych sieci VLAN?**

    Ponieważ interfejs F0/1 jest ustawiony jako trunk.

* **`S1# show vlan brief`**

    ```
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/7
                                                  Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                  Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                  Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                  Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                  Fa0/24, Gi0/1, Gi0/2
    10   Student                          active    Fa0/5, Fa0/6
    20   Faculty-Admin                    active
    1002 fddi-default                     act/unsup
    1003 token-ring-default               act/unsup
    1004 fddinet-default                  act/unsup
    1005 trnet-default                    act/unsup
    ```

* **Sprawdź połączenie między urządzeniami. Test komendą ping powinien powieść się pomiędzy wszystkimi urządzeniami**

    Urządzenia się pingują.

### Wyniki realizacji zadań - instrukcja 5.2.

#### Część 2. Konfiguracja sieci VLAN oraz łączy trunkowych na przełącznikach

##### Krok 1.

* **Na S1, skonfiguruj sieci VLAN wraz z ich nazwami podanymi w tabeli Specyfikacja portów na przełącznikach. Napisz poniżej, jakich komend użyłeś(aś):**

    ```
    # vlan 10
    # name Students
    # vlan 20
    # name Faculty
    # exit
    ```

* **Na S1, skonfiguruj interfejs podłączony do R2 jako łącze trunkowe. Skonfiguruj także interfejs podłączony do S2 jako łącze trunkowe. Napisz poniżej, jakich komend użyłeś(aś):**

    ```
    # int f0/1
    # switchport mode trunk
    # exit
    ```

* **Na S1, przypisz do sieci VLAN 10 port dostępowy, do którego podłączony jest PC-A. Napisz poniżej, jakich komend użyłeś(aś):**

    ```
    # int f0/6
    # switchport access vlan 10
    # switchport mode access
    # exit
    ```

##### Krok 2.

* **Na S2, upewnij się, że nazwy sieci VLAN oraz ich numery są zgodne z tymi na S1. Napisz poniżej, jakich komend użyłeś(aś):**

    `# show vlan brief`

#### Część 3. Konfiguracja routingu inter-VLAN 802.1Q opartego na łączach trunkowych

##### Krok 1.

* **Utwórz podinterfejs na R1 G0/1 dla VLAN 1, używając '1' jako identyfikatora podinterfejsu. Napisz poniżej, jakich komend użyłeś(aś):**

    `# interface g0/1.1`

* **Przypisz podinterfejs do VLAN 1. Napisz poniżej, jakich komend użyłeś(aś):**

    `# encap dot1Q 1`

* **Ustaw adres IP na podinterfejsie, zgodnie z Tabelą adresacji. Napisz poniżej, jakich komend użyłeś(aś):**

    `# ip address 192.168.1.1 255.255.255.0`

##### Krok 4.

* **Uruchom interfejs G0/1. Napisz poniżej, jakich komend użyłeś(aś):**

    ```
    # interface g0/1
    # no shutdown
    # exit
    ```

##### Krok 5.

* **Wpisz komendę pozwalającą na wyświetlenie tabeli routingu na R1. Które sieci zostały wyświetlone?**

    ```
    192.168.1.0/24
        192.168.1.0/24
    192.168.10.0/24
        192.168.10.0/24
    192.168.20.0/24
        192.168.20.0/24
    209.165.200.0/24
        209.165.200.224/27
    ```

* **Czy jest możliwe połączenie z PC-A, (komenda ping) z bramą domyślną VLAN 10?**
    Tak

* **Czy jest możliwe połączenie z PC-A (komenda ping) z PC-B?**
    Tak

* **Czy jest możliwe połączenie z PC-A (komenda ping) z Lo0?**
    Tak

* **Czy jest możliwe połączenie z PC-A (komenda ping) z S2?**
    Tak

### Wyniki realizacji zadań - instrukcja 5.3.

#### Część 2. Wykrywanie błędów w konfiguracjach routingu między sieciami VLAN

* **Na R1, wydaj komendę `show ip route` w celu podejrzenia tablicy routingu.
Które sieci zostały wylistowane?**

    ```
    192.168.1.0/24
        192.168.1.0/24
    192.168.10.0/24
        192.168.10.0/24
    192.168.20.0/24
        192.168.20.0/24
    209.165.200.0/24
        209.165.200.224/27
    ```

* **Czy brakuje niektórych sieci w tablicy routingu? Jeśli tak, jakie to sieci?**
    Nie

* **Na R1, wydaj komendę `show ip interface brief`. Na podstawie wyświetlonych rezultatów, odpowiedz czy pojawiły się jakieś problemy z interfejsami na routerze? Jeśli tak, które komendy rozwiążą problem?**

    ```
    Interface                  IP-Address      OK? Method Status                Protocol
    Embedded-Service-Engine0/0 unassigned      YES unset  administratively down down
    GigabitEthernet0/0         unassigned      YES manual administratively down down
    GigabitEthernet0/1         unassigned      YES manual up                    up  
    GigabitEthernet0/1.1       192.168.1.1     YES manual up                    up  
    GigabitEthernet0/1.10      192.168.10.1    YES manual up                    up  
    GigabitEthernet0/1.20      192.168.20.1    YES manual up                    up  
    Serial0/0/0                unassigned      YES unset  administratively down down
    Serial0/0/1                unassigned      YES unset  administratively down down
    Loopback0                  209.165.200.225 YES manual up                    up  
    ```
    Nie pojawiły się problemy.

#### Część 3. Sprawdzanie konfiguracji VLAN, przypisania portów i połączeń trunkowych

* **Na S1, wydaj komendę `show vlan brief`, aby wyświetlić bazę danych VLAN.
Które sieci VLAN zostały wylistowane? Zignoruj sieci VLAN 1002 do 1005.**

    ```
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/7
                                                  Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                  Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                  Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                  Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                  Fa0/24, Gi0/1, Gi0/2
    10   Students                         active    Fa0/6
    20   Faculty                          active
    ```

* **Czy istnieją jakieś sieci VLAN (nazwy albo same ich numery) nie wylistowane? Jeśli tak, podaj je.**
    Nie istnieją.

* **Czy porty dostępowe zostały przypisane do właściwych sieci VLAN? Jeśli nie, wypisz brakujące lub niewłaściwe przypisania.**
    Tak

* **Jeśli konieczne, napisz, które komendy mogą pomóc rozwiązać powyższe problemy z sieciami VLAN?**
    Nie było problemów.

* **Na S2, wydaj komendę `show vlan brief`, aby wyświetlić bazę danych VLAN.
Które sieci VLAN zostały wylistowane? Zignoruj sieci VLAN 1002 do 1005.**

    ```
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
                                                    Fa0/6, Fa0/7, Fa0/8, Fa0/9
                                                    Fa0/10, Fa0/11, Fa0/12, Fa0/13
                                                    Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                    Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                    Fa0/23, Fa0/24, Gi0/1, Gi0/2
    10   Student                          active
    20   Faculty                          active    Fa0/18
    ```

* **Czy istnieją jakieś sieci VLAN (nazwy albo same ich numery) nie wylistowane? Jeśli tak, podaj je.**
    Nie istnieją.

* **Czy porty dostępowe zostały przypisane do właściwych sieci VLAN? Jeśli nie, wypisz brakujące lub niewłaściwe przypisania.**
    Tak

* **Jeśli konieczne, napisz, które komendy mogą pomóc rozwiązać powyższe problemy z sieciami VLAN?**
    Nie było problemów.

* **Na S1, wydaj komendę `show interface trunk`, aby wyświetlić bazę danych VLAN.
Które porty są ustawione w trybie trunkowym?**

    ```
    Port        Mode             Encapsulation  Status        Native vlan
    Fa0/1       on               802.1q         trunking      1
    Fa0/5       on               802.1q         trunking      1
    ```

* **Czy któreś porty nie występują na liście? Jeśli tak, podaj je.**

    Inne porty nie są portami trunkowymi.

* **Jeśli konieczne, napisz, które komendy mogą pomóc rozwiązać powyższe problemy z portami trunkowymi?**

    Nie ma problemów.

* **Na S2, wydaj komendę `show interface trunk`, aby podejrzeć interfejsy trunkowe.
Które porty skonfigurowano jako trunkowe?**

    ```
    Port        Mode             Encapsulation  Status        Native vlan
    Fa0/1       on               802.1q         trunking      1
    ```

* **Czy w wyświetlonej informacji brakuje którychś portów? Jeśli tak, podaj je.**

    Inne porty nie są portami trunkowymi.

* **Jeśli konieczne, napisz, które komendy mogą pomóc rozwiązać powyższe problemy z portami trunkowymi?**

    Nie ma problemów.

#### Część 4. Testowanie łącza na Warstwie 3.

* **Z PC-A, czy jest możliwe połączenie (komenda ping) z bramą domyślną VLAN 10?**
    Tak

* **Z PC-A, czy jest możliwe połączenie (komenda ping) z PC-B?**
    Tak

* **Z PC-A, czy jest możliwe połączenie (komenda ping) z Lo0?**
    Tak

* **Z PC-A, czy jest możliwe połączenie (komenda ping) z S1?**
    Tak

* **Z PC-A, czy jest możliwe połączenie (komenda ping) z S2?**
    Tak

* **Z PC-A, czy jest możliwe połączenie (komenda ping) z S1?**
    Tak

* **Z PC-A, czy jest możliwe połączenie (komenda ping) z S2?**
    Tak

### Odpowiedzi na pytania - instrukcja 5.1.

1. **Jakie dostrzegasz korzyści ze stosowania tradycyjnego routingu między sieciami VLAN?**

    * Prostota konfiguracji

### Odpowiedzi na pytania - instrukcja 5.2.

1. **Jakie korzyści dostrzegasz ze stosowania routingu inter-VLAN 802.1Q opartego na łączach trunkowych?**

    * Możliwość lepszego wykorzystania potencjału VLAN poprzez łączenie między sobą wielu VLAN na pojedynczym łączu fizycznym
    * Odseparowanie routingu na poziomie IP od routingu na poziomie VLAN

### Odpowiedzi na pytania - instrukcja 5.3.

1. **W jakim sensie podgląd tablicy routingu może być pomocny w diagnozowaniu problemów sieciowych?**

    Zamiast diagnozowania stanu sieci metodą prób i błędów (tudzież tzw. 'czarnej skrzynki'), można na jednym listingu zobaczyć wszystkie dostępne z danego węzła trasy i wyciągnąć wnioski na temat wadliwie skonfigurowanych węzłów w sieci.
