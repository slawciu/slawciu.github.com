---
layout: post
title: ReactNative i MaterialUI
category: dajsiepoznac
comments: true
image: "/public/006 (Mobile).png"
date: 2017-03-15 22:25:00 0100
---

Uruchomiliśmy szkielet aplikacji. Swą spartańską urodą urzekła zapewne niejednego. Mnie nie ;) Dziś skupimy się na 2 rzeczach: nadaniu naszej aplikacji mobilnej stylu zbliżonego do [Material Design](https://material.io/guidelines/) i dorzucimy Navigator.

## Konfiguracja
Styl nadawać możemy ręcznie - wymyślając wygląd każdej nowej kontrolki, albo skorzystać z [gotowego rozwiązania](https://github.com/xotahal/react-native-material-ui). 

    yarn add react-native-material-ui

    react-native link react-native-vector-icons

Po wykonaniu powyższych poleceń musimy jeszcze dorzucić linijkę

    compile project(':react-native-vector-icons')

do pliku `build.gradle` w sekcji `dependencies`

Teraz możemy czerpać garściami z ostylowanych komponentów, o ile wcześniej poinformujemy ReactNative, gdzie je znajdzie

    import { COLOR, ThemeProvider, Toolbar } from 'react-native-material-ui';

## Użycie react-native-material-ui
Zaczniemy od `<ThemeProvider uiTheme={uiTheme}>`. Ten komponent opakuje nam całą aplikację (komponenty wewnątrz) w styl Material Design. Jako `prop` przekazujemy mu `uiTheme` - obiekt, za pomocą którego możemy dostosować styl do naszych potrzeb - ustawiając np. kolor przewodni aplikacji.

## Navigator
Wewnątrz `ThemeProvider` wrzucamy komponent `Navigator`.  Skorzystam z Navigatora dostępnego w samym ReactNative. [Tutaj](https://facebook.github.io/react-native/docs/navigation.html) możesz poczytać o innych opcjach. Navigator sam w sobie niczego nam nie narysuje (dopóki mu nie powiemy jak), ale sprawi, że poruszanie się między ekranami i co najważniejsze - zarządzanie tym procesem będzie o wiele prostsze w przyszłości. Musimy tylko zdefiniować ścieżki (`routes`), którymi będziemy się poruszać. Pierwszym przystankiem na naszej ścieżce będzie lista książek. 

    const routes = {
        home: {
            Title: 'Domowa Biblioteka',
            Page: BooksList
        }
    };


Skoro Navigator zna już ścieżki, powiedzmy mu, w jaki sposób ma nam je przedstawić.
Korzystamy z faktu, że elementowi ścieżki zdefiniowaliśmy komponent odpowiedzialny, więc wrzucamy ten komponent pomiędzy `<` i `>`. Magia, smrodek, kwiatek, herezja, gamechanger? Nazwij to jak chcesz - działa :).

    _renderScene(route, navigator) {
        return ( 
            <View>
                <route.page route={route} navigator={navigator}/>
            </View>
        );
    }

Teraz tylko wystarczy stworzyć komponent `BooksList`. Przy zacznę porządkować to, co ostatnio zostawiłem w kodzie - mały bałagan. Nowy komponent wyląduje w osobnym pliku. Rysując się wykorzysta `ListView` od facebooka i `Toolbar` z paczki Material Design. Dorzucimy jeszcze jakieś przykładowe dane i oto jest. Pierwszy kolorowy widok.

<img class="postImage" src="/public/006 (Mobile).png" />

Więcej kodziku z dzisiejszego posta znajdziesz na [githubie](https://github.com/slawciu/home-library/tree/master/HomeLibraryMobile).