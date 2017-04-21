---
layout: post
title: IT Science Fiction(?)
category: dajsiepoznac
comments: true
date: 2017-04-21 19:18:00 0100
---
Spisując rozważania na temat [“Czy studia są potrzebne programiście”](/dajsiepoznac/2017/03/09/czy-programista-potrzebuje-studiow/) przypomniałem sobie o pewnym micie noszącym miano “Projekt grupowy”. Projekt grupowy to taki projekt, do wykonania którego niezbędne jest utworzenie grupy ludzi. Ważne, by w tej grupie znalazła się osoba, która ten projekt wykona, by pozostałe mogły się go ewentualnie “nauczyć” i obronić - zaliczając tym samym przedmiot. 

##Projekt "grupawy"
Nauka pracy grupowej - niedokonana. Frustracja osoby, której zależy na dobrej ocenie i zrobi ten projekt samodzielnie - ogromna. Bardziej obrotne osoby dobierają się w grupy i tworzą ową grupą projekty na kilka przedmiotów - co kończy się zwykle podziałem zadań: 1 osoba - 1 przedmiot. Wszyscy podpisują się pod wszystkim - tu frustracja maleje, każdy coś robi, więc zasługuje przecież na ocenę… Nauka pracy grupowej - już lepiej, bo można zaobserwować element komunikacji w zespole i zbudowane zaufanie. A gdzie wiedza i umiejętności pracy nad 1 projektem w kilka osób? Brak. Wiedza i umiejętności, które wykorzystam w pracy? Nie ma.
Sam byłem świadkiem i członkiem opisanych grup, choć wcale mi się to nie podobało. Podoba mi się za to podejście: tylko konstruktywna krytyka…

##Projekt grupowy
W standardowym modelu oceniany jest przeważnie wynik projektu - co skutkuje tym, że ta jedna osoba robi go na noc przed oddaniem. Według mnie powinna być dodatkowo oceniana systematyczność i wkład w pracę poszczególnych osób. Jak to łatwo sprawdzić? - wykorzystując githuba albo inne ogólnodostępne uczelniane repozytorium. 
Zakładamy, że projekt polega na zakodzeniu jakiejś aplikacji. Każdy student powinien posiadać swoje własne konto i pushować swoją część kodziku. Ze strony prowadzącego przedmiot jedynym wysiłkiem musiałoby być jedynie sprawdzenie, kto, kiedy i jak często commitował. Dodatkowo przy okazji takiego projektu studenci mogliby przećwiczyć robienie Code Review. Można też dorzucać inne zabawki w postaci serwera CI albo Issue Trackera.
Przychodząc do pracy takie rzeczy nie będą nowością, tylko czymś, z czym miało się kontakt. Na koniec oceniana jest tylko praca kontrybutorów - osoby niewystępujące w logach mogą spróbować za rok... Oczywiście istnieje opcja commitowania przez 1 osobę na 4 czy 6 różnych kontach, ale pewnie i temu można sprytnie zaradzić.

##Egzamin z programowania na kartce
Wszyscy przez to przechodzili. Pilnowanie, by nikt nie miał dostępu do Internetu, co wymusza znajomość składni i nazw wszystkich metod i klas, które chcemy wykorzystać w kodzie. Jak to się ma do pracy? Niech pierwszy rzuci kamieniem, kto nigdy nie wszedł na stackoverflow, by zakodzić coś dla klienta. Co można zaproponować w tym miejscu?

##Egzaminy przy komputerach.
Zacznijmy od tego, że proces sprawdzania można zautomatyzować - pisząc odpowiednie testy, a studentom dając zadanie implementacji interfejsów, które to implementacje wstrzyknięte do gotowej aplikacji powinny skutkować określonym rezultatem. Bazę przypadków można przygotować wcześniej i sprawić, że nadal będzie można zrobić podział na grupy. I dajmy na to na ocenę 3: ma działać - tj testy mają być zielone. Na  wyższą ocenę - w rozwiązaniu powinien być zaimplementowany wskazany wzorzec projektowy. Dostęp do internetu - proszę bardzo, ale kosztem czasu na rozwiązanie - tak, by nie opłacało się przesyłać rozwiązań między sobą. W większości przypadków egzaminów “kartkowych” sam IntelliSense dostępny w IDE wiele by uprościł.

Zadziała?