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

## 15. Podać przykłady programów shell i ich właściwości?



## 16. W jaki sposób program shell interpretuje polecenie?



## 17. Na czym polega wykonywanie polecenia w tle (w drugim planie)?



## 18. Co to jest planowanie (szeregowanie) procesów?



## 19. Podać przykłady algorytmów szeregowania procesów i wyjaśnić ich działanie?



## 20. Jak rozwiązuje się zagadnienie planowania procesów w systemach typu UNIX?



## 21. Kiedy, po co i jak wykonywany jest proces ładowania systemu?



## 22. Jaki proces ma PID=1, jakie zadania wykonuje?



## 23. Co to są pliki i jakie typy plików występują w systemie UNIX?



## 24. Co to jest i-węzeł?



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
