---
layout: post
title: To uczucie, kiedy możesz sprawdzić, czym oddychasz...
category: dajsiepoznac
tags: [elektronika, smogomierz, grafana, influxdb, iot]
comments: true
image: "/public/024/01.png"
date: 2018-11-19 08:01:00 0100
---
Już podczas eventu w Katowicach, okazało się, że czujniki mierzące skład powietrza w tym samym pomieszczeniu podają różne odczyty. Dlatego zanim zapakujemy nasze czujniki do sugerowanego opakowania w postaci kolan kanalizacyjnych, pora na kilka testów.

## Praca w jednym miejscu
Pierwszy test - czujniki umieszczone są jeden obok drugiego, czas trwania testu 20 min, wprawne oko dowie się, gdzie ostatecznie znajdą się czujniki. Odczyty na wykresie.

<img class="postImage" style="width: 100%" src="/public/024/01.png" />

Wniosek 1: Powietrze w domu powyżej normy?!

Wniosek 2: Wskazania różnią się o 4 mikro gramy na metr sześcienny.

## Oczyszczacz powietrza
Czy na pewno działa? Czy też daje tylko poczucie świeżego powietrza na sam dźwięk pracującego w nim wentylatora? Jeden z czujników zmienia lokalizację, teraz będzie w pokoju z oczyszczaczem tuż obok niego.

<img class="postImage" style="width: 100%" src="/public/024/02.png" />

Wniosek 1: Różnica widoczna już na pierwszych kilku odczytach.

Wniosek 2: Wygląda na to, że nasz oczyszczacz powietrza działa - przynajmniej w drugim pokoju powietrze mieści się już w granicach normy.

## Oczyszczacz powietrza podejście 2
O 7:30 przenosimy oczyszczacz do pokoju z drugim czujnikiem (Imielin).

<img class="postImage" style="width: 100%" src="/public/024/03.png" />

Wniosek 1: widać tu, że sobie całkiem nieźle radzi. W ciągu kilku minut powietrze ma stężenie pyłów PM2.5 i PM10 mieszczące się w granicy normy europejskiej.

Wniosek 2: spadek stężenia pyłu z 28 na 10 ug/m^3 w niecałą godzinę

## Otwórzmy okno
Od 11:58 do pokoju bez oczyszczacza wpada powietrze z zewnątrz. 

<img class="postImage" style="width: 100%" src="/public/024/04.png" />

Wniosek: Jest ciepło, jak na listopad i nawet ocena wzrokowa nie wróży żadnych rewelacji - wykres lekko w górę.

## Antyperspirant w sprayu
Przy okazji - co się stanie, gdy rozpylimy antyperspirant w okolicy czujnika pyłów? To ta szpilka kilka minut po 9...

<img class="postImage" style="width: 100%" src="/public/024/06.png" />

## Czujnik bliżej otwartego okna

<img class="postImage" style="width: 100%" src="/public/024/05.png" />

Odczyty znacząco w górę, mimo nienajgorszej widoczności, ilość pyłów jest ponad kreską wyznaczającą normę.

Wniosek: Czas mija, ludzie wracają do domów i zaczynają dogrzewać okoliczne gospodarstwa… Pora zamknąć okno. Szansę na wietrzenie lepszym powietrzem można wykorzystać pracując z domu lub stosując jakąś automatykę, która nam uchyli okna. Można sprzęgnąć czujnik z domową automatyką - wietrzyć, gdy na zewnątrz jest lepsze powietrze (akurat jak jesteśmy w pracy)... I pojawia się luka szansa dla złodzieja! “Ogłupić” czujnik świeżym powietrzem i poczekać, aż okna same się uchylą…

## A co się dzieje w nocy?
Okna rozszczelnione.

<img class="postImage" style="width: 100%" src="/public/024/07.png" />

Wniosek 1: Na noc zamykamy okna i włączamy oczyszczacz. Koniecznie.

Wniosek 2: 9 listopada przenieśliśmy oba czujniki do tego samego pokoju - z oczyszczaczem. Wygładzenie wykresu za pomocą średniej kroczącej (10 ostatnich pomiarów). Widać wyraźnie, że odczyty PM2.5 są prawie identyczne, nadal występuje różnica przy PM10

## Podsumowanie
Zakup smogomierza w częściach przyniósł nie tylko frajdę w postaci zabawy z elektroniką (pamiętacie jeszcze [rzeczybezinternetu](http://rzeczybezinternetu.blogspot.com)?), ale też dał nam możliwość sprawdzenia wydajności naszego oczyszczacza powietrza. Niebawem elektronika wyląduje w sugerowanym opakowaniu i zostanie zamontowana na zewnątrz. Aż strach pomyśleć, co się pojawi na wykresach, gdy nadejdzie sroga zima...
