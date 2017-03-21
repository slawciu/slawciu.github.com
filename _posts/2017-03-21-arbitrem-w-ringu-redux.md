---
layout: post
title: Arbitrem w ringu Redux
category: dajsiepoznac
comments: true
image: "/public/007.png"
date: 2017-03-21 22:08:00 0100
---

##Redux
Rozwijając aplikację w duchu #yoloProgramming można łatwo skodzić swoje własne legacy, którego w życiu nie będziemy chcieli tknąć. Łatwo wpaść w tę pułapkę tworząc aplikacje w React, gdzie każdy komponent posiada swój własny stan, a my możemy wyczyniać z nim niestworzone rzeczy. Czas ukręcić na siebie bata i zapiąć do Domowej Biblioteki [Reduxa](https://github.com/reactjs/redux) - wariacji na temat [Fluxa](https://facebook.github.io/flux/), który delikatnie zmienia sposób, w jaki informacje przepływają przez aplikację.

![Redux - diagram](/public/007.png)

##Actions
Chcąc zmienić stan naszej aplikacji definiujemy akcję, która zostanie wywołana z poziomu komponentu (prawdopodobnie w wyniku interakcji z człowiekiem). Akcja przedstawia się typem i niesie ze sobą jakąś informację - tekst, liczbę, obiekt - cokolwiek wymyślimy. W tworzeniu akcji wg Reduxa powinni nam pomóc ActionCreators.

##Reducers
Skoro akcja opisuje zmianę, warto na nią zareagować. W tym celu posłuży nam <del>Manager</del> Reducer. Redux zakłada, że stan naszej aplikacji jest globalny - pozbywamy się `state` komponentu skąd tylko się da. Ponadto stan jako taki nie ulega zmianie - po każdej modyfikacji wynikającej z akcji mamy do czynienia z nowym stanem. Obiekty z rodziny Reducers posiadając informację o poprzednim stanie i dokonanej zmianie, tworzą nowy stan.

##Store
Nad wszystkim czuwa Store. Przechowuje stan aplikacji, umożliwia jego pobieranie i modyfikowanie. Ponadto przechowuje informację o subskrybentach zmian stanu aplikacji.

##Components
Wracamy do komponentów. Te w większości przypadków pozbawione stanu operują na danych dostępnych w `props`.

Na [githubie](https://github.com/slawciu/home-library/tree/master/HomeLibraryMobile) możesz zobaczyć, jak to wygląda w aplikacji mobilnej.
Przy ‘zapinaniu’ Reduxa korzystałem z [tutoriala](https://medium.com/@jonlebensold/getting-started-with-react-native-redux-2b01408c0053#.2ytogtjgv) - działa :)

Teraz już prosta droga do rozwijania funkcjonalności właściwych.
