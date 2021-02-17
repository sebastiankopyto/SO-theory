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



## 9. Jak proces jest kończony?
## 10. Jak działa funkcja systemowa exec?
## 11. Jak działa funkcja systemowa fork?
## 12. Co to są funkcje systemowe?
## 13. W jakich stanach może być proces?
## 14. Co to jest "shell"?
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
