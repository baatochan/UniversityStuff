# Rozległe sieci komputerowe

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-: | :-: | :-:
07.05.2018 07:30 | DHCP | Iwo Bujkiewicz (226203)<br />Bartosz Rodziewicz (226105)<br />Dominik Szymon Cecotka

### Odpowiedzi na pytania - instrukcja 11.1

1. Dlaczego podczas konfiguracji DHCPv4 wykluczamy statyczne adresy zanim skonfigurujemy pulę DHCPv4?  
	Nie wykluczenie ich spowodowałoby, że DHCP mógłby przydzielić je do hostów dynamicznych, co spowodowałoby konflikt adresów, bo dwa urządzenia miałyby ten sam adres.

1. Jeżeli istnieje wiele puli DHCPv4, jak przełącznik przypisuje informację IP do hosta?  
	Switch przypisze hostowi adres z puli, która przypisana jest do VLANu, do którego przypisany jest port do którego host jest podłączony.

1. Jakie funkcje poza przełączaniem może obsługiwać przełącznik Cisco 2960?  
	Switch może działać jako serwer DHCP i może zajmować się routingiem statycznym i między-VLANowym.

### Odpowiedzi na pytania - instrukcja 11.2

1. Jak myślisz czy użycie agenta DHCP relay ma zalety w stosunku do sytuacji gdy wiele routerów działa jako serwery DHCP?  
	Wykorzystanie wielu routerów jako serwerów DHCP zwiększyło by złożoność sieci oraz utrudniło możliwości centralnego zarządzania sieciom. Dodatkowo wymagało by aby każdy router wykonywał więcej pracy zarządzając swoim adresowaniem DHCP poza główną funkcją - routowania ruchu sieciowego.  
	Posiadanie jednego serwera DHCP w sieci ułatwia zarządzanie nią oraz sprawia, że sieć jest bardziej scentralizowana.

### Odpowiedzi na pytania - instrukcja 11.3

1. Jakie są zalety użycia DHCP?
	* Automatyzuje działanie sieci, gdy łączy się wiele różnych, nieznanych urządzeń
	* rozwiązuje konflikty adresów
	* może dostarczać dodatkowe wartości konfiguracyjne, jak adres serwera DNS

### Odpowiedzi na pytania - instrukcja 11.4

1. Która metoda adresowania IPv6 wykorzystuje więcej zasobów pamięci na routerze skonfigurowanym jako serwer DHCPv6, bezstanowy DHCPv6 czy stanowy DHCPv6? Dlaczego?  
	Stanowy DHCPv6 używa więcej zasobów pamięci. Wymaga on aby router przechowywał informacje o dynamicznym stanie klientów. Klienci bezstanowego DHCPv6 nie używają serwera DHCP do otrzymania informacji o adresie, więc te informacje nie muszą być przechowane.
	<!--
	Sprawdz czy dobrze to przetlumaczylem :|

	Stateful DHCPv6 uses more memory resources. Answers will vary, but Stateful DHCPv6 requires the router to store dynamic state information about the DHCPv6 clients. Stateless DHCPv6 clients do not use the DHCP server to obtain address information, so this information does not need to be stored.
	-->

1. Jaki rodzaj dynamicznego przypisywania adresów IPv6 jest zalecany przez Cisco, bezstanowy DHCPv6 czy stanowy DHCPv6?  
	Cisco zaleca bezstanowy DHCPv6.

### Odpowiedzi na pytania - instrukcja 11.5

1. Jaka komenda jest potrzebna w puli DHCPv6 dla stanowego DHCPv6, a nie jest potrzebna dla bezstanowego DHCPv6? Dlaczego?
	Komenda `ipv6 prefix address` jest potrzebna dla stanowego DHCPv6. Hosty otrzymują unikalny adres IPv6 od serwera DHCP, więc ta komenda jest potrzebna by ustawić jaki prefix IPv6 będzie używany w tej sieci.

1. Jaka komenda jest potrzebne na interfejsie, aby sprawić żeby sieć korzystała ze stanowego DHCPv6 zamiast z bezstanowego DHCPv6?
	Komenda `ipv6 nd managed-config-flag` jest używana by ustawić flagę stanowego DHCPv6. Jest ona przekazywana do wszystkich hostów za pomocą wiadomości RA routera.
