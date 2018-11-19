---
layout: post
title: Programowanie dynamiczne
category: dajsiepoznac
comments: true
date: 2017-04-13 20:32:00 0100
---
Szukając inspiracji dla kolejnego posta nieprojektowego, natknąłem się na twitterze na wpis o programowaniu dynamicznym. To mi przypomniało, że kiedyś na studiach popełniłem pewien artykuł na ten temat...

Programowanie dynamiczne – metoda rozwiązywania problemów charakteryzujących się optymalną podstrukturą (droga do rozwiązania problemu prowadzi poprzez optymalne rozwiązanie podproblemów tego samego typu) i wspólnymi podproblemami. Nazwa programowanie dynamiczne nie odnosi się bezpośrednio do programowania komputerów, oznacza rozwiązywanie problemów z życiem tablic. Metoda ta ma zastosowanie w tych algorytmach, w których zapamiętanie obliczonego już wyniku i odwołanie się do niego w dalszej części może znacznie usprawnić jego działanie – zmniejszyć złożoność i czas wykonania samego algorytmu. W ten sposób oszczędza się czas, który byłby  poświęcony na ponowne obliczanie tej samej wartości – w razie potrzeby odczytywana jest ona z pamięci. 

Programowanie dynamiczne stosujemy jako jedną z metod działania algorytmu obok m. in. rekursji lub metody dziel i zwyciężaj, przeważnie tam, gdzie jedna z tych metod zawodzi. Np. użycie metody dziel i zwyciężaj do obliczenia dwumianu Newtona przynosi skutek fatalny – ze względu na drzewiastą budowę drogi do rozwiązania wiele obliczeń powtarza się, zasoby są tracone na kilkakrotne obliczanie tej samej wartości. Chcąc obliczyć wartość wyrażenia <img class="postImage" src="/public/013/01.png" /> wspomnianą metodą (opierając się na zależności <img class="postImage" src="/public/013/02.png" /> gdzie <img class="postImage" src="/public/013/03.png" /> musimy obliczyć wartości kolejno <img class="postImage" src="/public/013/04.png" /> i  <img class="postImage" src="/public/013/05.png" /> żeby obliczyć te wartości należy obliczyć wyrażenia: dla  <img class="postImage" src="/public/013/06.png" /> więc pozostaje policzenie wartości  <img class="postImage" src="/public/013/07.png" /> – obie te wartości znamy, możemy policzyć drugą gałąź: dla  <img class="postImage" src="/public/013/08.png" /> – drugą wartość znamy (jest równa 1), pierwszą musimy policzyć, jednak warto zauważyć, że była ona już wcześniej liczona. Przy obliczaniu wartości dwumianów dla większych wartości n i k drzewo rozwiązania się rozrasta, zatem liczba duplikujących się obliczeń rośnie.

Z drugiej strony decydując się na użycie programowania dynamicznego jako podstawowej zasady działania algorytmu należy wziąć pod uwagę rozmiar danych wejściowych n, dla których obliczane będą przykładowe wartości. Zgodnie z ideą programowania dynamicznego potrzebna jest tablica do przechowywania obliczonych wartości. Im większe n, tym większa tablica, co z kolei wymaga większej ilości potrzebnej pamięci. Sposób rozwiązania problemu zależy od posiadanych przez nas zasobów – czasu i pamięci komputera. Zazwyczaj rozwiązanie znajdzie się gdzieś w środku przedziału między najlepszą szybkością, a małą ilością zajmowanego miejsca w pamięci.
Aby lepiej zobrazować zalety programowania dynamicznego, zaimplementowano w języku c++ poniższe algorytmy i przeprowadzono testy sprawdzające czas wykonania algorytmów dla konkretnych danych wejściowych i ilość wykonywanych wybranych operacji. Wyniki przedstawiono na wykresach.
 
## Programowanie dynamiczne a metoda dziel i zwyciężaj.
Algorytm obliczania dwumianu Newtona oparty o wzór
<img class="postImage" src="/public/013/09.png" />
 gdzie
<img class="postImage" src="/public/013/10.png" />

zaimplementowano ustawiając wartowników w miejscach występowania operacji przypisania i dodawania. 

Algorytm w oparciu o metodę dziel i zwyciężaj

<script src="https://gist.github.com/slawciu/efbde91b35c3de4a149700a6cc09cb16.js"></script>

Algorytm w oparciu o programowanie dynamiczne

<script src="https://gist.github.com/slawciu/54afcc8382b82fc1e14e29190ea8f731.js"></script>

Uruchomiono oba algorytmy w trybie Debug w programie Visual Studio 2008 na komputerze z procesorem IntelCore 2 Duo T5750 2.00GHz, 3GB RAM, Windows Vista. Otrzymane dane przedstawiono na wykresach. Aby obliczyć czas wykonania posłużono się funkcją clock() z biblioteki time.h.
 
 <img class="postImage" src="/public/013/w01.png" />
Kolorem niebieskim oznaczono wyniki dla algorytmu D&C. Czas wykonania algorytmu opartego o programowanie dynamiczne do zaprezentowanych n był mniejszy od tysięcznych części sekundy, wyniki są niewidoczne. Wyraźnie widać, że do n=27 nie ma prawie żadnej różnicy w czasie wykonania algorytmów, potem czas wykonania algorytmu D&C szybko rośnie.

 <img class="postImage" src="/public/013/w02.png" />
  <img class="postImage" src="/public/013/w03.png" /> 
 
Powyższe dwa wykresy prezentują zależność pomiędzy ilością wykonanych operacji: przypisania i dodawania dla algorytmu programowania dynamicznego; porównania dla algorytmu D&C a wielkością n. Na powyższym wykresie zaprezentowano powiększenie przedziału ilości operacji od 0-600. W tej skali widać, że w przeciwieństwie do algorytmu D&C (punkty w kształcie rombów) algorytm oparty o programowanie dynamiczne ma złożoność zbliżoną do liniowej, co więcej nachylenie przybliżonej prostej do osi OX jest niewielkie, co sugeruje, że dla większych wartości n  ilość wykonanych operacji będzie powoli liniowo wzrastać. Podkreślając tę zaletę nie należy jednak zapominać o wzrastającym zapotrzebowaniu na pamięć. Dla małych n (do 6) ilość wykonywanych operacji jest praktycznie taka sama.

 <img class="postImage" src="/public/013/w04.png" />

Powyżej przedstawiono zależność liczby operacji dodawania i przypisania od wielkości n dla algorytmu opartego o programowanie dynamiczne. Dla tej ilości danych już wyraźnie widać zakrzywienie, jednak w porównaniu z oczekiwaną ilością operacji dla algorytmu rekursywnego można przyjąć, że zależność ta jest nadal liniowa. Ilość operacji osiągnięta przez ten algorytm dla n=1650 odpowiada w przybliżeniu ilości operacji dla n=23 algorytmu rekursywnego.
 
## Programowanie dynamiczne a rekursja
Zaimplementowano algorytm obliczający kolejne wyrazy ciągu Fibonacciego w oparciu o wzór
<img class="postImage" src="/public/013/11.png" />
W języku C++, ustawiając wartowników w miejscach występowania operacji przypisania i dodawania. 
<script src="https://gist.github.com/slawciu/d2efb13e8870e65cc51bf835b7b18ceb.js"></script>

Dla programowania dynamicznego:

<script src="https://gist.github.com/slawciu/d0d5a06b8ccaf2a1b83d4060add134b0.js"></script>

 <img class="postImage" src="/public/013/w05.png" />

Na wykresie widać, że dla n większego od 40 czas wykonania algorytmu zaczyna gwałtownie rosnąć. Zaznaczono wyniki dla algorytmu rekursywnego, czas wykonania algorytmu opartego o programowanie dynamiczne ponownie w tym przedziale był zbyt niski, by program mógł go wychwycić (mniejszy od tysięcznej części sekundy).  

 <img class="postImage" src="/public/013/w06.png" />

  <img class="postImage" src="/public/013/w07.png" />

Powyższy wykres jest powiększeniem w dla n<=12. Widać, że dla n=4 algorytm rekursywny jest lepszy (liczba wykonanych operacji dominujących jest mniejsza), jednak wraz ze wzrostem n, czas jego wykonania rośnie gwałtownie szybko. Wykres nad nim obrazuje skalę przyrostu ilości operacji wraz ze wzrostem n.
 
Reasumując, programowanie dynamiczne w ogólnym przypadku możemy zastosować tam, gdzie dany rodzaj obliczeń jest wykonywany wielokrotnie dla tych samych danych i zapamiętanie raz policzonej wartości lub ogólnie wyniku danej operacji może być w przyszłości ponownie odczytany i użyty do dalszych obliczeń. Idea oparcia metody o tablicę powoduje, że dla większej ilości danych rośnie rozmiar programu w pamięci, dlatego sens użycia metody należy rozpatrywać również w kategoriach dostępnego sprzętu. Kryterium, którym będziemy się kierować wybierając tę metodę zależy od konkretnego przypadku.
Zestawienie programowania dynamicznego z metodą dziel i zwyciężaj oraz rekursją jednoznacznie pokazują, że programowanie dynamiczne może z sukcesem zastąpić wymienione wcześniej metody usprawniając czas wykonania algorytmu i znacznie redukując jego złożoność.