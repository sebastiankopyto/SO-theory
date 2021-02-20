## 1. Co to jest system operacyjny?
Program pośredniczący między systemem komputerowym a użytkownikiem.
<br />
<br />
Zadania systemu operacyjnego:
* Obsługa zadań użytkownika jako procesów
* Przydzielanie procesom zasobów komputera: dostępu do jednostki centralnej, pamięci, dysków itd.
<br />

## 2. Co oznacza wielodostępność, a co wielozadaniowość? 

**Wielodostępność** - wielu użytkowników pracujących z jednym komputerem, sprawia wrażenie samodzielnej pracy 
<br />
**Wielozadaniowość** - Każdy użytkownik może uruchomić jednocześnie wiele programów
<br />
<br />

## 3. Jakie funkcje spełnia wielodostępny system operacyjny i jakie podsystemy wchodzą w jego skład?

Podsystemy wykonujące zadania:
* **Zarządzanie procesami** - tworzenie, usuwanie, zawieszanie, odwieszanie procesow, mechanizmy synchronizacji procesów, komunikacja między procesami
* **Zarządzanie pamięcią** - zarządzanie pamięcią główną, obszarem wymiany (swap), pojęcie pamięci wirtualnej
* **Zarządzanie przestrzenią dyskową** - zarządzanie wolną przestrzenią dysków, procesami, zapisywanie informacji na dysku, szeregowanie zadań zapisu i odczytu
* **Zarządzanie operacjami wejścia/wyjścia** - obejmuje podsystem buforowania, interfejs: urządzenia - sterowniki, sterowniki urządzeń
* **Zarządzanie plikami** - tworzenie, usuwanie plików i katalogów, elementarne operacje z plikami i katalogami
* **Podsystem ochrony** - ochrona procesów przed działaniem innych procesów; mechanizmy zapewniające, że pliki, segmenty pamięci, CPU, inne zasoby są udostępnione tylko tym procesom, które mają autoryzacje systemu operacyjnego. Ogólnie: mechanizmy kontroli dostępu programów, procesów, użytkowników do zasobów systemu komputerowego.
* **Praca sieciowa** - usługi umożliwiające komunikację w sieci, pojęcie systemów rozproszonych
<br />

## 4. Co jest przedmiotem standaryzacji w wielodostępnych systemach operacyjnych?

* przenośność aplikacji (**portability**)
* możliwość współpracy oprogramowania działającego na różnych maszynach (**interoperability**)
* skalowaność (**scalability**) - możliwość rozbudowy sprzętowej i rozbudowy aplikacji bez konieczności zmian systemu

**Główna istota standardu**: określenie interfejsu, a nie implementacji.
<br />


## 5. Co to jest proces?

Proces jest to wykonywnay program. <br />
Składa się z kodu progrmau i przydzielonego mu obszaru pamięci. <br />
Program, zawarty w pliku przechowywanym na dysku, ma charkater bierny. Proces z licznikiem rozkazów określającym kolejny rozkaz do wykonania ma charakter aktywny. Ten sam program może być wykonywany jako kilka niezależnych procesów, np. program vi wywołany przez dwóch użytkowników.
<br />

## 6. Co to jest blok kontrolny procesu i do czego służy?

Zawiera informacje obejmujące:
* **Stan procesu** 
* **Licznik rozkazów** - wskazuje adres następnej instrukcji do wykonania
* **Rejestry procesora** - w zależności od architektury komputera: akumulatory, rejestry indeksowe, wskaźniki stosu, rejestry ogólnego przeznaczenia, rejestry warunków. Blok kontrolny zawiera informacje pamiętane w rejestrach w celu kontynuacji wykonywania procesu po przerwaniu.
* **Informacje związane z planowaniem przydziału czasu procesora** - priorytet procesu, wskaźniki do kolejek porządkujących, inne parametry
* **Informacje dotyczące zarządzania pamięcią**
* **Informacje do rozliczeń** - zużyty czas procesora, czas rzeczywisty, ograniczenia czasu, numery konta, zadań, procesów
* **Informacje o stanie opacji wejścia wyjścia** - lista otwartych plików, wykaz urządzeń przydzielonych do procesu, informacja o niezrealizowanych zamówieniach na operacje wejścia/wyjścia.
<br />

## 7. Co oznacza współbieżne wykonywanie procesów?

W systemie wielodostępnym, pracującym z podziałem czasu, jest jednocześnie wiele procesów. Procesy działają współbieżnie, co oznacza konieczność podziału zdolności obliczeniowej procesora (przełączanie) między poszczególne procesy, ponieważ w każdej chwili czasu wykonywany jest tylko jeden proces. Proces wykonywany jest w sposób sekwencyjny, tzn. w każdej chwili na zamówienie procesu wykonywany jest jeden rozkaz kodu programu.
<br />

## 8. Jak powstaje nowy proces?

<a name="fork"></a>
* Nowy proces tworzony jest rzez wywolanie funkcji _fork_
* Proces wywołujący te funkcję nazywany jest **procesem macierzystym**, a proces utworzony **potomkiem**
* Potomek uzyskuje pozycję w tablicy procesów
* Proces uzyskuje **identyfikator** (PID)
* Tworzona jest kopia kontekstu macierzystego (nowy proces zawiera kopię przestrzeni adresowej procesu macierzystego)
* Uaktualnione zostają liczniki odwołań do plików ii-węzłów, z którymi związany jest potomek
* Identyikator potomka przekazywany jest procesowi macierzystemu
* Potomek dziedziczy prawa dostępu do otwartych plików, a także dzieli dostęp do plików. Procesy mają identyczne kopie segmentów instrukcji, danych i stosu
* Po wykonaniu funkcji _fork_ wywoływana jest zwykle funkcja _exec_
* Służy do wykonania określonego, innego programu. Umieszcza w obszarze pamięci procesu kopię pliku wykonywalnego i rozpoczyna jego wykonywanie. Zawartość kontekstu (obraz pamięci) procesu wywołującego funkcję exec zostaje zamazana.

<br>

**Tworzenie nowego procesu przy wykonywaniu polecenia zewnętrznego**

* Proces to wykonywany program, tzn program, który został rozpoczęty i jeszcze nie zakończył się.
* Proces składa się z kodu programu i przydzielonego mu obszaru pamięci.
* Polecenie wykonywane jest dwuetapowo
* Tworzony jest nowy proces (proces potomka), który ma wykonywać polecenie; jest to kopia bieżącego procesu. Mechanizm ten nosi nazwę rozwidalnia (fork, forking a process)
* Nowy proces jest przekształcany w proces wykonujący polecenie; mechanizm nosi nazwę wykonywania (executing a command)
* Dziedziczone przez proces potomny środowisko obejmuje informacje o właścicielu i grupie o standardowych strumieniach, do ktorych przyłączony jest terminal, otwartych plikach, bieżącym katalogu i zmiennych globalnych
<br>

## 9. Jak proces jest kończony?

**Kończenie procesu przez użytkownika**<br>
Proces można przerwać wysyłając do niego odpowiedni sygnał. Można w tym celu skorzystać z polecenia **kill**, które powoduje wysyłanie sygnałów do procesów.<br>
_kill [-s nazwa sygnału | numer sygnału] PID [PID ...]_<br>
gdzie PID to identyfikator procesu.<br>
Polecenie **kill**, w którym pominięto nazwę i numer sygnału wysyła do wskazanego procesu sygnał o numerze 15 (SIGTERM). Taki sygnał może być przechwycony, zignorowany lub zablokowany.<br>
Sygnałem którego nie można przechwycić, zignorować ani zablokować jest sygnał o numerze 9 (SIGTERM). <br>
Polecenie:<br>
  _kill -9 PID_<br>
  zawsze zakończy proces o podanym PID.<br>
**Przykłady sygnałów**<br>
* 1 HUP zerwanie łączności
* 2 INT przerwanie (wysyłany również z klawiatur: Ctrl + C)
* 3 QUIT zakończenie (wysyłany również z klawiatury: Ctrl + \\)
* 9 KILL bezwarunkowe zakończenie procesu
* 15 TERM programowe zakończenie procesu

<br><br>

**Naturalne kończenie wykonywania procesu**<br>
Proces kończy się w naturalny sposób, gdy wykona ostatnią instrukcję, wywołuje wtedy funkcję _exit_. <br>
Proces przechodzi do stanu zombi, zwalnia swoje zasoby i oczyszcza kontekst, za wyjątkiem pozycji w tablicy procesów.<br>
Proces macierzysty czekający na zakończenie potomka wykonuje funkcję _wait_.<br>
Jądro szuka potomków takiego procesu, bedących w stanie zombi - jeśli znajdzie, to przekazuje PID potomka oraz parametr funkcji _exit_ i dostarcza do procesu macierzystego.<br>
Proces macierzysty uzyskuje ifnromacje, który z wielu możliwych potomków zakończył pracę. <br>
Jądro zwalnia następnie pozycję procesu potomnego w tablicy procesów.

<br>

## 10. Jak działa funkcja systemowa exec?

Służy do wykonania określonego, innego programu. Umieszcza w obszarze pamięci procesu kopię pliku wykonywalnego i rozpoczyna jego wykonywanie. Zawartość kontekstu (obraz pamięci) procesu wywołującego funkcję exec zostaje zamazana.

## 11. Jak działa funkcja systemowa fork?

Funkcja systemowa powodująca, że proces wywołujący tę funkcję ulega w chwili jej wywołania podziałowi (albo „rozwidleniu”, ang. fork) na dwa procesy (innymi słowy – tworzony jest nowy proces). O jednym z tych procesów mówi się „proces-rodzic” (ang. parent process) a o drugim – „proces potomny” (lub czasem „potomek”, „proces-dziecko”, ang. child process).<br>

[Jak powstaje proces](#fork)
<br>

## 12. Co to są funkcje systemowe?

Interfejs między procesami i systemem operacyjnym. Zawierają odwołania do systemu (API).
<br>

## 13. W jakich stanach może być proces?

* **nowy** - proces jest tworzony
* **wykonywany** - 
  * **w trybie użytkownika** - wykonywane są instrukcje
  * **w trybie jądra** - wykonywane sa instrukcje
* **gotowy** do wykonania - proces czeka na przydział procesora przez program szeregujący, w tym stanie jest zwykle wiele procesów
* **czekający** (uśpiony) - proces czeka na wystąpienie zdarzenia niezbędnego do jego dalszego wykonywnaia, np. na zakończenie operacji wejścia/wyjścia
* **zakończony** - proceszakończył wykonywanie
<br>

## 14. Co to jest "shell"?

Program, który pośredniczy pomiędzy jądrem, systemem plików i programami usługowymi.

1. Użytkownik
   1. Wprowadza polecenie
2. Shell
   1. Czyta wiersz polecenia
   2. Przetwarza wiersz polecenia
   3. Tworzy proces
3. Unix
   1. Wykonuje proces

<br>

**Podstawowe funkcje shella**<br>
* Przekazywanie sterowania do programu wybranego poleceniem użytkownika
* Wykonywanie wbudowanych poleceń
* Dostarczenie języka do pisania skryptów
* Ustawianie środowiska pracy
* Przywoływanie i edycja uprzednio wydanych poleceń
* Przeadresowywanie wejścia - wyjścia poleceń
* Generowanie nazw plików
* Umożliwienie łączenia poleceń w potok
* Umożliwienie przetwarzania w drugim planie (nie interakcyjnie)

## 15. Podać przykłady programów shell i ich właściwości?



## 16. W jaki sposób program shell interpretuje polecenie?

**Polecenia proste**

1. Interpretator wczytuje wiersz poleceń z pliku standardowego (terminala) i interpretuje go.
2. Interpretator (shel) wykonuje rozwidlenie (fork).
3. Następnie wykonuje funkcję wait
4. Wykonywana jest funkcja exec w odniesienio do procesu potomnego i proces ten wykonuje polecenie (program) umieszczone w wierszu polecenia.
5. Po tym czasie interpretator czeka na zakończenie procesu potomnego
6. Po jego zakończeniu wczytuje kolejne polecenie.

**Uwaga**<br>
W przypadku poleceń wbudowanych (cd, for, while) interpretator wykonuje je bezpośrednio bez tworzenia nowych procesów.
<br><br>

**Polecenia ze zmianą standardowego pliku wyjściowego**
<br>
np. ls -l > lista <br>

1. Proces potomny tworzy plik lista.
2. Jeśli próba utworzenia pliku nie powiedzie się, to proces potomny kończy działanie.
3. Jeśli plik zostanie utworzony, proces potomny zamyka standardowy plik wyjściowy i powiela deskryptor nowego.
4. Po zapisaniu informacji, zamika plik wyjściowy i kończy działanie.
<br><br>

**Wykonywanie polecenia w tle** <br>
np. grep user * > lista & <br>
1. Interpretator rozpoznaje w wierszu polecenia znak & (przetwarzanie w tle).
2. Ustawia odpowiednią zmienną lokalną
3. Pod koniec pętli sprawdza jej wartość i jeśli jest ustawiona to nie wykonuje funkcji wait, ale przechodzi do początku pętli i wczytuje następne polecenie
<br><br>

**Polecenie z potokiem** <br>
np. ls -l | wc <br>
1. Interpretator wykonuje funkcje **fork** i tworzy proces potomny **wc**
2. Proces potomny tworzy potok **pipe** i wywołuje funkcję **fork** tworząc swojego potomka
3. Proces ten (wnuk interpretatora) wykonuje pierwszą część polecenia (ls)
4. W celu pisania do potoku, zamyka deskryptor pliku standardowego
5. Powiela deskryptor potoku do pisania, a następnie zamyka go
6. Proces (wc) zamyka swój standardowy plik wejściowy, a powiela deskryptor potoku do czytania
7. Po przeczytaniu zamyka deskryptr potoku i wykonuje polecenie wc
8. Interpretator wraca do początku pętli

<br>

## 17. Na czym polega wykonywanie polecenia w tle (w drugim planie)?


## 18. Co to jest planowanie (szeregowanie) procesów?

Polega na określaniu w jakiej kolejności procesy uzyskują dostęp do zasobów komputera: procesora, pamięci operacyjnej. <br>
Celem planowania jest zwykle zapewnienie jak najlepszego wykorzystania procesora.<br><br>
Procesy starając się o dostęp do procesora czy konkretnego urządzenia czekają w kolejkach
* kolejka zadań
* kolejka procesów gotowych do procesora
* kolejki do urządzeń wejścia/wyjścia
Wykonywany proces może:
* Zażądać operacji wejścia/wyjścia - zostanie wtedy umieszczony w kolejce do urządzenia wejścia/wyjścia
* utworzyć nowy proces i czekać na jego ukończenie
* wykorystać cały kwant czasu lub w wyniku przerwania zostać przeniesiony do kolejki procesów gotowych

<br><br>

**Kryteria planowania**
1. Wykorzystanie procesora, w % czasu
2. Przepustowość - liczba procesów kończonych w jednostce czasu
3. Czas cyklu przetwarzania - średni czas przetwarzania procesu od chwili utworzenia do zakończenia
4. Czas odpowiedzi - średni czasoczekiwania w kolejkach
5. Czas odpowiedzi - w systemach interakcyjnych - czas między zgłoszeniem zamówienia przez użytkownika a pierwszą odpowiedzią.
<br> 

## 19. Podać przykłady algorytmów szeregowania procesów i wyjaśnić ich działanie?

* **FCFS (First Come, First Served)** - pierwszy nadszedł - pierwszy obsłużony. Realizowany za pomocą kolejki FIFO. Wady: efekt konwoju, kłopotliwy w systemach z podziałem czasu. Jest algorytmem niewywłaszczającym.
* **SJF (Shortest Job First)** - najpierw najkrótsze zadanie. Procesor przydzielany jest procesowi o najkrótszej następnej fazie procesora. Teoretycznie daje minimalny średni czas oczekiwania. Wymaga jednak dokładnego oszacowania czasu przyszłej fazy procesora dla każdego procesu. Szacowanie to wykonywane jest zwykle na podstawie pomiarów czasu faz poprzednich. Może być wywłaszczający lub nie.
* **Planowanie priorytetowe** - każdemu procesowi jest przydzielany pewien priorytet. Wybierany jest proces o najwyższym priorytecie. Algorytm SJF jest szczególnym przypadkiem. Może być wywłaszczającym lub nie.
* **Planowanie rotacyjne** - zaprojektowany dla systemów z podziałem czasu. Ustalony jest kwant czasu (10-100 ms). Kolejka procesów ma charakter cykliczny. Kolejnym procesom przydzielany jest co najwyżej kwant czasu.
* **Przełączanie kontekstu** - obejmuje czynności związane z przechowaniem stanu (informacji wskazanych w bloku kontrolnym) starego procesu i załadowania stanu procesu nowego. Czas przełączania kontekstu (rzędu 1-100 us) istotnie wpływa na wydajność systemu.

<br>

## 20. Jak rozwiązuje się zagadnienie planowania procesów w systemach typu UNIX?

* System z podziałem czasu - jądro przydziela procesor gotowemu procesowi na jeden kwant czasu - zgodnie z algorytmem rotacyjnym
* Po upływie tego czasu wywłaszcza proces i przydziela procesor procesowi następnemu w kolejce. Wybiera proces załadowany do pamięci o najwyższym priorytecie
* Jądro okresowo przelicza i modyfikuje priorytety wszystkich procesów gotowych
* Wywłaszczony proces jest umieszczany w jednej z kolejek priorytetorywch i gdy przyjdzie na niego kolej - jest wznawiany od miejsca, w którym nastąpiło zawieszenie wykonywania

## 21. Kiedy, po co i jak wykonywany jest proces ładowania systemu?

* Celem procesu ładowanie jest umieszczenie systemu operacyjnego w pamięci operacyjnej i rozpoczęcie jego wykonywania.
* Składa się z kilku etapów:
  1. Inicjalizacja i testowanie sprzętu
  2. Wczytywanie i umieszczenie w pamięci bloku systemowego (blok **0**) z dysku
  3. Program zawarty w bloku systemowym ładuje jądro systemu operacyjnego z pliku systemowego (np. **/stand/vmunix**) do pamięci. Przekazuje sterowanie do pierwszej instrukcji jądra. Program jądra systemu zaczyna się wykonywać.
  4. Wykrywanie i konfiguracja urządzeń, odnalezienie głównego katalogu plików.
  5. Przygotowanie środowiska procesu **0**. Wykonywanie programu systemu jako procesu **0** wykonywanego w trybie jądra. Utworzenie procesów jądra, np. procesów zarządzania pamięcią
  6. Rozwidlenie procesu **0** (wywołanie funkcji fork z jądra). Utworzony proces **1** tworzy kontekst poziomu użytkownika i przechodzi do trybu użytkownika
  7. Proces **1** wywołuje funkcję systemową exec wykonując program **/sbin/init**
  8. Proces **init** wczytuje plik **/etc/inittab** i rozmnaża procesy
  9. Inicjacja wewnętrzych struktur danych jądra, tworzenie np. listy wolnych buforów, i-węzłów, kolejek, inicjacja struktur segmentów i tablic stron pamięci
  10. Sprawdzenie głównego i pozostałych systemów plików (ew. uruchomienie fsck).
  11. Wywoływane są procesy **getty** monitorujące konsole i terminale systemu komputerowego, zgodnie z deklaracjami w pliku **inittab**, a proces **init** wykonuje funkcję systemową **wait** monitorując zakończenie procesów potomnych. Proces **init** tworzy również procesy demony.

## 22. Jaki proces ma PID=1, jakie zadania wykonuje?

1. Rozwidlenie procesu **0** (wywołanie funkcji fork z jądra). Utworzony proces **1** tworzy kontekst poziomu użytkownika i przechodzi do trybu użytkownika
2. Proces **1** wywołuje funkcję systemową exec wykonując program **/sbin/init**
3. Proces **init** wczytuje plik **/etc/inittab** i rozmnaża procesy
4. Inicjacja wewnętrzych struktur danych jądra, tworzenie np. listy wolnych buforów, i-węzłów, kolejek, inicjacja struktur segmentów i tablic stron pamięci
5. Sprawdzenie głównego i pozostałych systemów plików (ew. uruchomienie fsck).
6. Wywoływane są procesy **getty** monitorujące konsole i terminale systemu komputerowego, zgodnie z deklaracjami w pliku **inittab**, a proces **init** wykonuje funkcję systemową **wait** monitorując zakończenie procesów potomnych. Proces **init** tworzy również procesy demony.

## 23. Co to są pliki i jakie typy plików występują w systemie UNIX?

Pliki - jednostki logiczne przechowywanej informacji, niezależne od właściwosci fizycznych urządzeń pamięciowych Zwykle w plikach przechowywane są programy lub dane (tekst, liczby, grafika, itp.).
<br><br>

**Podstawowe typy plików**
* pliki zwykłe
* pliki specjalne
* katalogi
* dowiązania symboliczne
* potoki nazwane FIFO (named pipe)
* gniazda (UNIX--domain sockets)

## 24. Co to jest i-węzeł?

Rekord przechowujący większośc informacji o pliku

## 25. Jakie informacje są przechowywane w i-węźle?



## 26. Jakie informacje przechowywane są w pliku typu "katalog"?



## 27. Co to jest katalog z punktu widzenia użytkownika, a co z punktu widzenia budowy systemu plików?



## 28. Jaka jest różnica między adresowaniem bezpośrednim a adresowaniem pośrednim?



## 29. Wyjaśnić mechanizm rozmieszczania bloków i fragmentów pliku w blokach na dysku?



## 30. Jak adresowane są bloki i fragmenty pliku na dysku?



## 31. Czym różni się przydział ciągły miejsca na dysku od przydziału listowego?



## 32. Co to jest tablica FAT?



## 33. Porównać przydział listowy miejsca na dysku z przydziałem indeksowym?



## 34. Co to jest i jak jest wykorzystywana pamięć operacyjna?



## 35. Wyjaśnić mechanizm wymiany (swapping) procesów?



## 36. Wyjaśnić mechanizm stronicowania na żądanie?



## 37. Wyjaśnić mechanizm segmentacji?



## 38. Podać przykłady algorytmów wymiany stron?



## 39. Kiedy występuje błąd strony i jak jest obsługiwany?



## 40. Na czym polega zarządzanie pamięcią wykonywane przez system operacyjny?



## 41. Jakie są zadania podsystemu wejście - wyjście?



## 42. Co to są pliki specjalne i do czego służą?



## 43. Co to jest tablica rozdzielcza urządzeń we-wy, jakie informacje zawiera i do czego służy?



## 44. Jak wykorzystywana jest pamięć podręczna do wydajniejszego korzystania z systemów dyskowych?



## 45. Jakie są typy plików specjalnych?



## 46. Jakie informacje są zapisane w plikach specjalnych i do czego służą?



## 47. Jaką rolę pełnią podprogramy obsługi urządzeń?



## 48. Co to jest pamięć współdzielona?
