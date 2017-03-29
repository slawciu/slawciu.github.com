---
layout: post
title: Lokalizacja wewnątrz budynków
category: dajsiepoznac
comments: true
date: 2017-03-29 18:00:00 0100
---

Będąc na studiach przekonałem się, że informatyka to nie tylko wynik wyświetlony na ekranie po 4 godzinach pracy jakiegoś złożonego algorytmu. W dzisiejszych czasach możemy się na nią natknąć na każdym kroku. Informatyka wpływa na życie ludzi. Nie zawsze pozytywnie. Dziś trochę o lokalizacji wewnątrz budynków - dziedzina tak ekscytująca, że stała się tematem mojej pracy magisterskiej.

##Nawigacja a lokalizacja
Na początku rozdzielmy 2 rzeczy: nawigację i lokalizację - nawigacja to proces rozpoczynający się zdefiniowaniem punktów, między którymi chcemy znaleźć drogę, wytyczenie ścieżki między zdefiniowanymi punktami i ciągła informacja zwrotna - czy podążam założoną ścieżką, czy też zboczyłem z drogi i muszę na nią wrócić. Lokalizacja to określenie pozycji. Nawigacja korzysta z lokalizacji.

##Za firewallem
Jak działa lokalizacja na zewnątrz (GPS)? W dużym uproszczeniu pobieramy dane o naszym położeniu z satelit umieszczonych na orbicie okołoziemskiej. Im więcej satelit - tym dokładniejsze koordynaty naszej pozycji jesteśmy w stanie uzyskać. W budynkach jest gorzej, bo ściany najzwyczajniej w świecie tworzą barierę prawie nie do przedarcia dla sygnału z satelit. Ogromna wada budynków.

Czy zastanawialiście się kiedyś, skąd gołębie wiedzą, w którą stronę powinny zmierzać, by dotrzeć do założonego celu? Google Maps Pigeon odpada - ciężko operować aplikacją i jednocześnie machać skrzydłami. Poza tym gołębie potrafiły przenosić listy na długo przed stworzeniem Internetu. Niektóre zwierzęta nauczyły się korzystać z pola magnetycznego, które wytwarza kula ziemska. Z podstawówki wiemy, że Ziemia to taki wielki magnes z 2 biegunami. Gołębie, langusty i kto wie co jeszcze wykorzystywały możliwość ‘odczytu’ pola magnetycznego i na jego podstawie udawały się w długie wędrówki.

##Pole magnetyczne + zakłócenia = ????
Pole magnetyczne działa do dziś, a budynki ze względu na materiały użyte podczas budowy zakłócają je w specyficzny sposób. I robią to na tyle sprytnie, że w ramach jednego budynku, godząc się na niewielki błąd pomiarowy jesteśmy w stanie jednoznacznie określić, gdzie aktualnie się znajdujemy. W ten sposób wielka wada w rozwiązaniu GPS stała się wielką zaletą. Co ciekawe, nie tylko budynki zakłócają pole magnetyczne. Analogiczne zjawisko możemy zaobserwować w kopalniach rud metali.

Zwierzęta już dawno poradziły sobie z odczytaniem tej niewidzialnej siły - człowiek też - tylko trochę później. Mało tego, przy odrobinie szczęścia posiadasz taki czytnik przy sobie. Gdzie? W Twoim telefonie komórkowym. Magnetometr jest wykorzystywany jako część układu odpowiadającego za orientację telefonu. Korzysta z niego aplikacja kompas i wszystkie kompasopochodne (live view Flightradara, Sky Map od Google’a). Możesz z niego skorzystać i Ty - na Androidzie jest to dziecinnie proste - wystarczy się ‘zapisać’ na zdarzenia generowane przez [czujnik](https://developer.android.com/reference/android/hardware/Sensor.html#TYPE_MAGNETIC_FIELD) i z określoną częstotliwością będziemy otrzymywać wartości (x,y lub x,y,z w zależności od modelu) natężenia pola magnetycznego w mikro Teslach.

##Pod dachem
I znów w dużym uproszczeniu - żeby dowiedzieć się, gdzie się znajdujemy w danym budynku, ktoś musi wcześniej go zmapować - za firewallem zajmują się tym kartografowie - w budynku wystarczy, że osoba wyposażona w smartfon i odpowiednią aplikację przespaceruje się po miejscach, które chcemy objąć zasięgiem systemu lokalizacji - w ten sposób powstanie mapa pola magnetycznego budynku. Potem już zwykły użytkownik będzie mógł odpalić swoją aplikację i posiadając informację o mapie zobaczyć, w którym miejscu się znajduje. Lokalizacja zaimplementowana - można ją wstrzyknąć do modułu nawigacji i zacząć na tym zarabiać.

Btw - myśleliście, jak w dzisiejszych czasach można zrealizować [Mapę Huncwotów (ang. Marauder's Map) ](https://www.youtube.com/watch?v=onm3sqQ4LMo)?