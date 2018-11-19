---
layout: post
title: Coraz bliżej backendu
category: dajsiepoznac
comments: true
image: "/public/014.png"
date: 2017-04-13 21:29:00 0100
---
Zeskanowanie kodu ISBN to dopiero pierwszy krok. Naszym celem jest uzyskanie informacji o książce jak najmniejszym kosztem - gdzie walutą jest czas spędzony nad katalogowaniem naszych wolumenów. Posiadając kod ISBN możemy odpytać jeden z serwisów udostępniających dane o książkach. Badając dostępne API doszedłem do wniosku, że najlepszym sposobem będzie odpytywać kilka serwisów i dostarczać na telefon wszystkie znalezione paczki informacji - to użytkownik wybierze najbardziej kompletną/prawidłową.
Dziś przygotujemy teren pod otrzymane z serwera dane na temat książki o zeskanowanym kodzie ISBN.

## Miejsce na nowe dane
Potrzebna będzie prosta formatka, która wyświetli się po otrzymaniu danych z serwera i umożliwi prezentację tych danych. Na chwilę obecną zupełnie wystarczające będą Tytuł, Autor i kod ISBN

<img class="postImage" src="/public/014.png" />

## Stan globalny a stan lokalny
Podczas tworzenia komponentu wprowadzimy w pola dane uzyskane z propsów. Zostały tam przepisane z globalnego stanu aplikacji. Od teraz będziemy nimi operować lokalnie - będą częścią stanu komponentu `NewBookForm`.

<script src="https://gist.github.com/slawciu/25fcf121c3ac11fd8613e232df25565c.js"></script>

## Kilka spostrzeżeń
Przy okazji ustawimy akcję przycisku Back na wywołanie ekranu skanowania kodu ISBN. Zwróć uwagę, że zamiast dotychczasowych push/pop wywołuję metodę replace. Replace zamienia aktualną ścieżkę `Navigatora` na podaną jako parametr. Co w ten sposób uzyskuję? Między innymi to, że aparat mam uruchomiony tylko w momencie skanowania (nie zostaje działać w tle). Ponadto przechodząc z ekranu skanowania do ekranu formularza komponent `Camera` nadal działał i możliwe było skanowanie kolejnych kodów… Nie będziemy implementować takiego ficzera :)

<script src="https://gist.github.com/slawciu/07fc7c30e800a58881e9164e43fe8d24.js"></script>

Metoda `onChangeText` komponentu `TextInput` “podmienia” tekst trzymany w stanie aplikacji na ten właśnie wprowadzony przez użytkownika. Po wprowadzeniu wszystkich danych wyślemy dane do huba - wykonując tap na `ActionButton`, do którego podepniemy odpowiednią akcję.