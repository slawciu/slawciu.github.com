---
layout: post
title: Czas spłacić dług
category: dajsiepoznac
comments: true
image: "/public/015-1.png"
date: 2017-04-21 17:29:00 0100
---
Jak dotąd większość czasu poświęciłem na rozwój części mobilnej całego systemu. Nie zapominajmy, że sama aplikacja mobilna jest tylko interfejsem między człowiekiem a właściwą magią, która sprawi, że to wszystko będzie działać.

##\#yolo
Dotychczas serwer był rozwijany w myśl słynnego ostatnio #yoloProgramming. Chodziło o to, żeby powstał działający szkielet backendu, do którego aplikacja mobilna będzie mogła się odzywać za pośrednictwem sieci.

##Testy
Czas spłacić dług techniczny, który został zaciągnięty i złożyć kilka unit testów w ofierze bogom programowania. Będzie to pierwszy krok do refaktoru kodziku napisanego w starym dobrym C#. Do napisania testów użyję frameworka [xUnit](https://xunit.github.io/), a same testy uruchamiał będę resharperowym [runnerem](https://github.com/xunit/resharper-xunit) (którego trzeba doinstalować).

<img class="postImage" src="/public/015-1.png" />

W widoku testów w solucji będziemy chcieli osiągnąć następującą sytuację:

<img class="postImage" src="/public/015-2.png" />

Zanim o implementacji - trochę o strukturze. Odkąd zacząłem swoją przygodę z unit testami, w głowie utkwił mi taki schemat: skoro testuję klasę `LibraryHub`, to muszę stworzyć klasę zawierającą testy: `LibraryHubTests`, a w środku napisać testy właściwe w myśl konwencji: `Should<do-something>When<describe-current-situation-here>`. I wszystko szło gładko, do czasu aż zestaw testów nie zawierał ściany `Should`-ów z przyrostkami definiującymi przypadki, w jakich dziać się powinny poszczególne rzeczy. W widoku testów nie było to czytelne. Jakiś czas poznałem inny sposób, w jaki można zaprojektować testy - tworząc z nich drzewko. Wtedy w widoku testów najpierw widzimy sytuacje, których dotyczą same testy, a rozwijając węzeł sytuacji widzimy test poszczególnych zachowań. Póki co nie znalazłem lepszej alternatywy - zatem do dzieła.

#Kodzik
Żeby osiągnąć zamiar z poprzedniego akapitu - zamiast tworzyć jedną klasę testującą - LibraryHubTests - tworzymy 2 `WhenGetLibraryStateCalled` oraz `WhenIsbnScannedCalled`. Wewnątrz napiszemy testy dla sytuacji, gdy na Hubie zostanie wykonana - w pierwszym przypadku metoda `GetLibraryState`, w drugim metoda `IsbnScanned`. Skupmy się na pierwszym przypadku. Moją intencją jest chęć posiadania pewności :), że po wykonaniu metody GetLibraryState na obiekcie reprezentującym rzecz, która ‘zawołała’ tą metodę zostanie wykonana metoda `updateLibraryState`. I tu pojawia się pytanie - jak to sprawdzić. Możemy na szybko napisać testowego klienta, który będzie się łączył do huba - ale w tym celu konieczne będzie uruchamianie całej aplikacji - bez sensu. Oczywistą drogą wydają się być mocki. Zamockujmy zatem potencjalnego `Callera` i zdefiniujmy mu akcję `updateLibraryState`, w której będziemy mogli wpłynąć na zmienne wewnątrz testu, które to z kolei będziemy mogli sprawdzać w asercji:
<script src="https://gist.github.com/slawciu/9d482055b56df3eb938f4986fcb89ece.js"></script>

Testowany kod:

<script src="https://gist.github.com/slawciu/a6bfa7116415327de85eb071c09a1a79.js"></script>

Zielono! Czas na refactor! Aktualny wygląd huba i klasy testującej znajdziesz na moim [githubie](https://github.com/slawciu/home-library). 

Jako funboy nUnita pokuszę się jeszcze o kilka spostrzeżeń zaobserwowanych podczas przesiadki: nUnit wymagał atrybutu `[SetUp]` przed metodą inicjalizującą test (co powodowało konieczność stworzenia takiej metody w każdej klasie z testami) - w xUnit załatwi nam to konstruktor - niesamowite w swej prostocie - 1 atrybut mniej. nUnitowy `[Test]` to `[Fact]`. Asserty są bardzo podobne - szczegółowy opis i więcej porównań znajdziesz oczywiście w [dokumentacji](https://xunit.github.io/docs/comparisons.html).