---
layout: post
title: Czas decyzji
category: dajsiepoznac
comments: true
date: 2017-04-27 19:24:00 0100
---

Projekt wkroczył w etap, w którym trzeba podjąć decyzję o tym, jak informacje będą przekazywane wewnątrz systemu. U bram huba stoi aplikacja mobilna i łaskawie czeka, aż ktoś obsłuży jej zapytanie odnośnie stanu biblioteki. Ta sama aplikacja jest też w stanie zażądać odnalezienie książki, której ISBN w pocie procka zeskanowała z książki umieszczonej w świecie niedostatecznego światła i nie wiadomo jakich jeszcze niebezpieczeństw…

Chcąc przećwiczyć podejście CQRS i zamknąć drogę klasie `SuperHelpfulManagerUtil2.cs`. Zdecydowałem, że do huba zostaną wstrzyknięte handlery odpowiedzialne dokładnie za 1 akcję. Handler zaimplementuje prosty interface, który pozwoli zdefiniować typ, jaki obsługuje dany handler i typ, jaki dany handler zwróci wyniku wykonania metody Handle:

<script src="https://gist.github.com/slawciu/89fc09e60f84c5cc946ed49f2eac3882.js"></script>

Problem może się pojawić, gdy w mój hub będzie wymagał podjęcia większej ilości akcji - ale w myśl zasady “Problemy rozwiązujmy jak się pojawią” - rozwiążemy ten problem jak się pojawi :). To podejście podpatrzyłem u [Marcina Bałdy na githubie](https://github.com/mbalda/bookstore) - spodobało mi się, polecam, implementuję:

<script src="https://gist.github.com/slawciu/37dad131eafd28a7eb09edde6e066b26.js"></script>

...być może w przyszłości pokuszę się o refactor...

Klasa implementująca interfejs będzie miała wstrzyknięte repozytorium - w ten sposób załatwimy dostęp do bazy. 
Hub będzie wiedział, że jest jakiś byt, który obsłuży jego chęć wykonania akcji. Wspomniany byt będzie wiedział, skąd ma wziąć dane do wykonania (repozytorium), ba może nawet skorzysta z innych bytów, które zrobią część pracy za niego. Repozytorium posiądzie wiedzę, czy dane obecnie trzymamy na statycznej liście, czy już może w bazie danych. Nikt nie wie za dużo, a wszyscy wykonują swoją pracę. Na chwilę obecną brzmi spoko. Do roboty!