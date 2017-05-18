---
layout: post
title: Konfiguracja per środowisko w ReactNative
category: dajsiepoznac
comments: true
date: 2017-05-18 21:00:00 0100
---
Informacje, którymi nie warto się dzielić znaleźć się mogą także w plikach projektu mobilnego. Oprócz tego możemy trafić na wszelkie zmienne zależne od środowiska, w którym chcemy uruchomić aplikację (adres serwera), klucz do api, z którego korzystamy bezpośrednio na telefonie i czego sobie tylko dusza developera zamarzy.

I w przypadku tworzenia aplikacji w ReactNative nie pozostajemy bez wsparcia w tej trudnej sytuacji. Wpisując słowa kluczowe `reactnative config`, możemy odnaleźć paczkę:

[react-native-config](https://github.com/luggit/react-native-config),

która rozwiąże wszystkie nasze problemy :)

W celu skorzystania z biblioteki musimy ją oczywiście zainstalować, następnie w głównym katalogu aplikacji mobilnej utworzyć plik .env (tworząc plik o nazwie `.env.` w eksploratorze windows lub korzystając z konsoli - wtedy bez sztuczek), w którym zawrzemy wszelkie interesujące nas dane, zależne od środowiska. Podobnie jak w ostatnim przypadku, warto dorzucić ten plik do .gitignore’a i zostawić sample’a na repo.

Korzystając z `react-native-config` możemy działać na wielu różnych plikach konfiguracyjnych. Obok .env możemy utworzyć .env.prod, .env.test, a przed zbudowaniem projektu wskazać ten, z którego dane powinny być dostępne w aplikacji. Jedyna niedogodność tej biblioteki jest taka, że nazwę pliku konfiguracyjnego wpisujemy do zmiennej środowiskowej ENVFILE, którą wcześniej musimy utworzyć w systemie. Chcąc zbudować aplikację wykorzystując plik .env, w konsoli wpisujemy zatem:

`set ENVFILE=.env & react-native run-android`

Konsola powie nam, który plik wykorzystujemy, a następnie zbuduje aplikację. Proste! Teraz możemy napisać skrypty, które przygotują nam aplikację dla różnych środowisk. Co ciekawe, react-native-config udostępnia dane z pliku konfiguracyjnego także dla kodu napisanego w javie - możemy więc z łatwością ładować zmienne konfiguracyjne zarówno w plikach z rozszerzeniem .jsx jak i .java. Jak korzystam z danych zapisanych plikach konfiguracyjnych? Sprawdź w [repo](https://github.com/slawciu/home-library/blob/master/HomeLibraryMobile/lib/signalrClient.js).