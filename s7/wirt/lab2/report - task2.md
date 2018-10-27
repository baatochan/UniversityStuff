### Zadanie 2 - Badanie kosztów środowiska z maszynami wirtualnymi

#### Obciążenie hosta poprzez maszyny wirtualne

Obciążenie procesora hosta przy pojedynczej maszynie widać na poniższym screenie.

![Jedna maszyna](screenshots/task2/ladowanie-maszyny-wirt-z-win.png)

Wynik dla dwóch maszyn wygląda następująco.

![Dwie maszyny](screenshots/task2/ladowanie-dwoch-maszyn-wirt-z-win.png)

#### Wykonanie testów
Instrukcja do tego ćwiczenia bardzo nieprecyzyjnie opisywała scenariusz testów. Z jednej strony zachęcani byliśmy do testowania na KVM, jednak do KVM nie mieliśmy przygotowanych maszyn z Windowsem. Z drugiej instrukcja była pisana tak jakby była przygotowana pod Windowsa jako system hosta. Dodatkowo nie mieliśmy podanych żadnych narzędzi benchmarkowych, które działają jednocześnie pod Linuxem i pod Windowsem, a więc dane z takich testów byłyby niemożliwe do porównania. To wszystko

Scenariusz na który się zdecydowaliśmy to wykonanie kilku testów w domu na naszych prywatnych komputerach.

Narzędziem służącym do obsługi wirtualnych maszyn był VirtualBox. Narzędziem benchmarkowym y-cruncher. W każdym wypadku wykonywaliśmy jeden i taki sam test - dziesięciokrotne liczenie 50 milionów cyfr rozwinięcia dziesiętnego liczby pi.

#### Omówienie wyników

W sprawozdaniu nie załączamy wszystkich wyników, a jedynie przetworzone na procentowe dane na wykresach. Prezentują się one następująco.

![Jedna maszyna](screenshots/task2/wyniki1.png)
![Dwie maszyny](screenshots/task2/wyniki2.png)

Na wynikach zauważana jest tendencja, że Linux jest lżejszym systemem przez co lepiej radzi sobie przy emulacji.

Natomiast jeśli chodzi o dość znaczy spadek mocy w komputerze drugim wydaje mi się, że wynika to z różnic pomiędzy tymi dwoma komputerami.

Pierwszy PC posiada dwurdzeniowy, dwu wątkowy procesor o taktowaniu 4.2GHz. Drugi natomiast posiada 4 rdzeniowy, 8 wątkowy procesor, ale o taktowaniu tylko 2.4GHz. Wydaje mi się, że y-cruncher radzi sobie o wiele lepiej z rozłożeniem obliczeń na wiele wątków, niż VirtualBox, który musi rozłożyć całą maszynę.
