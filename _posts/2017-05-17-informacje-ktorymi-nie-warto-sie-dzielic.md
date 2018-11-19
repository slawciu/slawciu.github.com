---
layout: post
title: Informacje, którymi nie warto się dzielić
category: dajsiepoznac
comments: true
date: 2017-05-17 19:36:00 0100
---
Tworząc oprogramowanie prędzej czy później dotrzemy do momentu, że gdzieś w repozytorium pojawią się nam dane, którymi nie chcielibyśmy się dzielić z całym światem: connection string do bazy danych, nasz klucz prywatny do zewnętrznego api. W idealnym świecie takie informacje nie powinny leżeć nigdzie na repo z kodzikiem. Połączenie z bazą danych powinno być załatwione przez serwer CI (konfigurację możemy trzymać na INNYM - niepublicznym - repozytorium), na pewno znajdzie się też sposób na wstrzyknięcie innych ustawień. Jednak co zrobić w przypadku, gdy nasze repozytorium leży na githubie, stawianie CI mija się z celem, bo projekt jest na tyle mały, że nakład pracy włożony w postawienie kolejnej instancji TeamCity zwróci się po długim czasie, a kodzik musi leżeć w publicznym miejscu?

Wtedy warto ukryć wrażliwe dane przed światem - najlepiej na maszynie developerskiej i nie chwalić się nimi na lewo i prawo. Dotychczas w Domowej Bibliotece connection string i klucz prywatny do Books api leżały sobie w repozytorium, co było bardzo nieodpowiedzialne z mojej strony. Klucz dezaktywowałem, teraz czas zabezpieczyć się przed podobnymi wpadkami w przyszłości.

## connectionStrings.config
W świecie .NETa możemy śmiało wyodrębniać poszczególne składowe app i web configów do osobnych plików. Jedyne, co musimy zrobić, to wskazać, gdzie znajduje się właściwa konfiguracja, kodzikiem mówiąc:

<script src="https://gist.github.com/slawciu/61e1a1dd40455d155621dab7c3f594a6.js"></script>

zamieniamy na

<script src="https://gist.github.com/slawciu/039efa92d385a409960acbe5c9db97c1.js"></script>

a we wskazanym pliku umieszczamy nasze connection stringi. Proste! Tak samo można postąpić z pozostałymi częściami web/app configa (np. wydzielając appSettings). Skoro już mowa o connectionStringach. Może się zdarzyć, że będziemy chcieli posiadać informację o sposobie łączenia do bazy danych w wielu miejscach. Problem? Skądże znowu! W każdym projekcie wymagającym połączenia do bazy wstawiamy connectionStringa, a jak się zmieni… Problem, bo trzeba zmieniać w wielu miejscach. Rozwiązanie? Umieść plik connectionStrings.config w katalogu Configuration, a w miejscach, gdzie plik musi się znajdować wewnątrz projektu (np. w przypdaku web site’ów) dodaj go do tego projektu JAKO LINK - (PPM -> Add Existing Item):

<img class="postImage" src="/public/021.png" />

## apiKeys.config
Sprawa się nieco komplikuje w momencie, gdy chcemy zrobić coś niestandardowego - np. swój własny typ konfiguracyjny. Klucze do api mógłbym trzymać w sekcji appSettings, ale wtedy musiałbym ukryć cały ten plik przed potencjalnymi kontrybutorami, a tego nie chcę robić. Dlatego też klucze do api będą posiadać swoją własną sekcję w konfiguracji, którą to sekcję będzie można wyodrębnić do osobnego pliku. Chcąc stworzyć nową sekcję, musimy stworzyć klasę dziedziczącą po ConfigurationSection, a w niej umieszczamy logikę odpowiedzialną za pobieranie danych z naszej sekcji. 

<script src="https://gist.github.com/slawciu/fa522a5581202f6a2c81ac723c81c8ef.js"></script>

Następnie rejestrujemy sekcję w pliku konfiguracyjnym i posiadając wszystkie wymagane glejty możemy śmiało wpisywać nasze tajne informacje do kolejnego xml’a - apiKeys.config i obowiązkowo dopisać go do .gitignore. 

Btw, zastanawialiście się kiedyś, jak stworzyć plik .gitignore w eksploratorze windows? “Nie, bo zawsze kopiowałem z innego projektu... lol” - eksplorator nie pozwoli nam utworzyć pliku o nazwie “.gitignore”, bo brakuje mu rozszerzenia, z chęcią natomiast utworzy plik o nazwie “.gitignore.” - logiczne ;)! 

By nie zostawić potencjalnych towarzyszy od kodu w niekomfortowej sytuacji, w której musieliby zgadywać, co powinno się znaleźć w nieobecnych plikach konfiguracyjnych, możemy dodać przykładowe pliki z konfiguracją (apiKeys.sample.config) i wrzucić je na repo.

<script src="https://gist.github.com/slawciu/dd8f96e0194a9fd3ac01455b1191bd70.js"></script>

Moje klucze są bezpieczne na mojej maszynie, a w repo leżą przykładowe pliki. I co najważniejsze - pobierając źródła na inną maszynę VS nie krzyczy o brakujące pliki. 