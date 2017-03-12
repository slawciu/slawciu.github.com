---
layout: post
title: HomeLibrary intro!
category: dajsiepoznac
comments: true
image: "/public/001.jpg"
date: 2017-03-01 20:15:00 0100
---

##Opis domeny
Wyobraź sobie, że Twój księgozbiór osiągnął rozmiar, którego nie sposób zmieścić na jednym regale w jednym pokoju. Dorzuć do tego fakt, że wyprowadzasz się z domu, a pośród książek znajdują się w nim pozycje, po które sięgasz częściej - Gra Endera i przyległości, przygody Inkwizytora Mordimera Madderdina i kilka innych... więc część książek zabierasz ze sobą. Czy wspomniałem już, że kolekcjonujesz całe serie książek? A serie mają to do siebie, że mogą być kontynuowane po latach oczekiwania na kolejną część. Nie martw się, w okolicy księgozbioru są 3 osoby, które szybko i chętnie uzupełniają brakujące tomy (zarówno te nowe, jak i te starsze, bo właśnie ukazało się tłumaczenie książki z 1992 roku). Idylla. 

Do czasu, aż okazuje się, że wiele z tomów posiadasz w 2 lub więcej kopiach i nie jest powiedziane, że nie pojawią się kolejne - po prostu nie sposób spamiętać, czy dany egzemplarz jest w lokalizacji bazowej księgozbioru, czy po prostu w aktualnym miejscu zamieszkania jednego z opiekunów… Zasada jest prosta - widzę na półce ostatni egzemplarz, a nie ma go u mnie - kupuję! Jakby tego było mało, pojawiają się też znajomi o zbieżnych z Twoimi gustach czytelniczych, więc dzielisz się z nimi swoimi papierowymi dobrami i starasz się zapamiętać co, kto, kiedy…

<img class="postImage" src="/public/001.jpg" />

Po kilku latach zaczynają doskwierać problemy:

1. Jakie ja właściwie mam książki?
2. Gdzie jest książka X?
3. Kto pożyczył moją książkę?
4. Można to skatalogować, ale to przecież zajmie tyle czasu...

Które prostym zabiegiem zamieniamy w wyzwania...

##Co może Ci pomóc w <del>rozwiązaniu tych problemów</del> podjęciu tych wyzwań? 
Proste, Kodzik! I same książki, które opatrzone są swego rodzaju identyfikatorem - ISBN - czy unikalnym? Cóż… z tym bywa różnie. Kod ISBN wydrukowany jest na każdej książce w Polsce od 1974, w nowszych wydawnictwach nie tylko jako ciąg cyfr, ale też jako kod paskowy. Dreszcz ekscytacji? 
Kod kreskowy możemy zeskanować skanerem takim jak w sklepie - albo wykorzystując do tego kamerę naszego telefonu. Posiadając numer ISBN i połączenie z Internetem możemy pobrać informacje o naszej książce - tytuł, autora, wydawnictwo, krótki opis, a jak będziemy mieć odrobinę szczęścia, to nawet okładkę.

##Tech-mięsko tutaj
Skoro księgozbiór okazuje chęć współpracy, trzeba jeszcze wybrać technologię. Testy zaplecza napiszę w C#, wykorzystując xUnit, sam backend również w starym dobrym C#, hostując rozwiązanie w chmurze Azure. Przyda się webowy podgląd na książki w sytemie - ReactJS, a skoro już mamy podwaliny ASPowej aplikacji, można użyć ReactJS.net. 

Do sqlowej bazy - grzecznie, za pomocą EntityFramework, a wszystkie zależności rozwiąże Autofac.
ISBN dostanie się do systemu za pośrednictwem telefonu z Androidem. Aplikacja zostanie napisana w multiplatformowym (bo 2 to już multi, a 8 użytkowników Windows Phone’a jakoś przełknie brak wsparcia - są przyzwyczajeni…) ReactNative.
