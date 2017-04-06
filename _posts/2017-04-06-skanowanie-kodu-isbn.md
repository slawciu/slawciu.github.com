---
layout: post
title: Skanowanie kodu ISBN
category: dajsiepoznac
comments: true
image: "/public/011.png"
date: 2017-04-06 14:40:00 0100
---
Jedną z kluczowych funkcjonalności aplikacji mobilnej będzie skanowanie kodu ISBN z książki. Kod ISBN to ten sam kod, który jest skanowany przy kasie, gdy kupujemy książkę.

##Historia
_"Czy to prawda, że w Moskwie na placu Czerwonym rozdają Samochody? Tak, to prawda, tylko że nie w Moskwie, lecz w Leningradzie, i nie na placu Czerwonym, a na placu Rewolucji, i nie Samochody, a rowery, i nie rozdają, a kradną."_

Teza: Wg wikipedii, ISBN jest niepowtarzalnym 13-cyfrowym identyfikatorem książki. Jako międzynarodowy standard został zatwierdzony w 1970 roku 

Tak, ale…

* do 31 grudnia ISBN składał się z 10 cyfr
* w Polsce nadawany jest od 1974 roku, a norma powstała w 1982 roku
* książka może być wydana bez numeru ISBN (wtedy jest obciążana 23% VATem - zamiast niższym na książki)
* zdarzają się duplikaty:
_“Norma nie wskazuje jednoznacznie, jak należy postąpić w takiej sytuacji, a o przyjętym rozwiązaniu wydawca decyduje na własną odpowiedzialność.(...) Jeśli książka została już wprowadzona do sprzedaży, nie ma możliwości naprawienia błędu. W publicznym obiegu będą znajdowały się dwie książki oznaczone tym samym numerem ISBN. Dlatego też prosimy o skrupulatne sprawdzanie numeru ISBN, który ma być wydrukowany na książce, tak aby unikać sytuacji osygnowania książki zdublowanym lub błędnym numerem.”_
[źródło](https://e-isbn.pl/IsbnWeb/start/poco.html)

Wniosek - odobnie jak z numerem [PESEL](http://www.polskieradio.pl/9/307/Artykul/1005998,Ten-sam-PESEL-dla-dwoch-roznych-osob-MSW-to-niemozliwe) - tu też nie będzie tak różowo.

##Kolejna biblioteka w Bibliotece
Problemy będziemy rozwiązywać jak się pojawią. Tymczasem czas zapiąć kolejną bibliotekę do naszej aplikacji (wspominałem już, że praca z ReactNative to jak zabawa klockami LEGO?) [react-native-camera](https://github.com/lwansbrough/react-native-camera). Biblioteka, która nie tylko umożliwi nam skanowanie kodów, ale też w przyszłości posłuży nam do robienia zdjęć książkom (w celu jednoznacznego określenia jej stanu).

Użycie jest banalnie proste. Najpierw przedstawmy kamerę naszej aplikacji:

`import Camera from 'react-native-camera';`

potem wykorzystajmy kodzik z przykładu na githubie, delikatnie dostosowując go do naszych potrzeb

<script src="https://gist.github.com/slawciu/c6e8eac135b0972371356180a477643a.js"></script>

Teraz tylko wystarczy uruchomić aplikację i skierować aparat w kierunku kodu ISBN - i oto jest! Pojawia się na androidowym Toast. Zeskanowany numer możemy przesłać na serwer...

<img class="postImage" src="/public/011.png" />