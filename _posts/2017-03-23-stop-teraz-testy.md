---
layout: post
title: Stop! Teraz testy
category: dajsiepoznac
comments: true
date: 2017-03-23 22:00:00 0100
image: '/public/008.png'
---
Po dość owocnym okresie tworzenia kodziku wyrzuty sumienia zaczynają gryźć niemiłosiernie, a widmo zbliżającej się klęski majaczy się na horyzoncie. O czym mowa - proste o projekcie bez testów. Po stronie mobilnej tworzenie aplikacji przypomina bardzo długiego spike’a, którego zadowalające (mnie) efekty lądują w repozytorium. Jako że szkielet aplikacji jest gotowy, czas dodać testy, które pokryją kodzik…

## \_\_test\_\_
Katalog o wiele mówiącej nazwie jest częścią template’a, który tworzy się za pomocą komendy `react-native init`. Znajdują się w nim 2 pliki testujące przykładowy kodzik na platformę Android i iOS. Mnie się nie przydadzą, więc wylatują. Na ich miejsce pojawi się kod testujący Reducery, Actions i Components. Jako że Redux leci z nami, testowanie powinno być błahostką.

## Jest
Facebook tworząc Reacta nie zapomniał o jednej z ważniejszych części życia oprogramowania (i dewelopera :)) - o testowaniu - i przygotował całkiem wygodną bibliotekę (sami określają ją mianem Painless JavaScript Testing). Painless i JavaScript? Sprawdźmy ten oksymoron. Na pierwszy ogień idzie Reducer. Będzie stosunkowo łatwy do przetestowania, gdyż przetwarza informację zawartą w otrzymanym obiekcie Action, transformując stan aplikacji.

Kod odpowiedzialny za obsługę zmiany stanu połączenia z hubem signalR:

<script src="https://gist.github.com/slawciu/f8ffd8081f27b328ee7401b20f6eaed7.js"></script>

Możemy przetestować tak:

<script src="https://gist.github.com/slawciu/d068cf58162a82fa27f8c39c9a66bd1a.js"></script>

Urzeka fluent api i mnogość funkcji sprawdzających efekt testów. Na pokładzie biblioteki znajdziemy funkcje sprawdzające obiekty jak i obiekty, programista .net odnajdzie też odpowiedniki assertów ze swojej ulubionej biblioteki na [N](https://www.nunit.org/) czy [x](https://xunit.github.io/). Oczywiście Jest posiada obszerną [dokumentację](https://facebook.github.io/jest/). Wspomniałem już o możliwości mockowania? Nic tylko brać i testować.

Żeby uruchomić nasze testy wystarczy w konsoli uruchomić magiczną komendę `npm test`

<img class="postImage" src="/public/008.png" />