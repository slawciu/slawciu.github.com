---
layout: post
title: Drugie spotkanie Microsoft Azure User Group na Śląsku
category: dajsiepoznac
comments: true
date: 2017-04-27 13:00:00 0100
---
26.04.2017 odbyło się 2 spotkanie grupy Azure. Tym razem swoją wiedzą podzielili się [Bartosz Sobczyk](@bsobczyk) - opowiedział o Active Directory i przyległościach w Azure i [Tomasz Krawczyk](https://www.future-processing.pl/blog/tkrawczyk-2/) - opowiedział o swoich doświadczeniach z Azure Data Lake


##Bartosz Sobczyk - Zarządzanie tożsamością na platformie Microsoft Azure
Active Directory nigdy nie leżało blisko moich kręgów zainteresowań. W ramach zaliczenia jednego z przedmiotów na studiach musiałem skonfigurować prostą domenę - sprowadziło się to do postawienia kontrolera domeny na jednej maszynie wirtualnej i wpięcie do niej dwóch innych maszyn wirtualnych. Przy okazji poznałem teorię, jaka za praktyką, której mogłem ‘dotknąć’ w pracy - już jako użytkownik, nie domorosły administrator.
Ale co to ma wspólnego z Azure? Azure udostępnia usługę Active Directory. Ba! Możemy w łatwy sposób zmigrować naszą lokalną domenę do chmury i korzystać ze wszystkich dobrodziejstw tego rozwiązania. Bartek bardzo obszernie opowiedział o możliwościach, jakie nam daje taka migracja. Z ciekawszych rzeczy, out of the box mamy integrację z popularnymi serwisami świadczących usługi uwierzytelniające - np. z Facebookiem - w ramach [Azure Active Directory B2C](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview). Integracja z istniejącymi aplikacjami wydaje się być całkiem prosta - wszystkie potrzebne informacje znajdziemy w dokumentacji. Skoro już mowa o integracji z aplikacjami - azurowe AD pozwoli nam zrzucić z siebie konieczność implementacji systemu uprawnień użytkowników, funkcjonalności resetowania haseł, czy w końcu trzymania tych haseł na serwerach i konieczności dbania o ich bezpieczeństwo w ramach aplikacji 
W ramach chmurowego AD Microsoftu możemy też uruchomić usługę [Conditional Access](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access), w które która gdzieś w środku jest w stanie korzystając z nauczania maszynowego rozpoznawać zachowania użytkownika niepasujące do wzorca logowania - np. logowanie z różnych lokalizacji w krótkim czasie. W ramach Conditional Access jesteśmy w stanie określić polityki logowania zależne od lokalizacji, z której użytkownik chce się zalogować do naszej usług np. z wewnątrz sieci firmowej wymagać tylko loginu i hasła, a spoza dodatkowo kodu przesłanego SMSem.


##Tomasz Krawczyk - Analiza Big Data z Azure Data Lake
Tomasz zaczął swoją prezentację od przypomnienia, ile to Zetabajtów danych ludzkość będzie posiadać za 3 lata. Posłużył się ciekawym sposobem zobrazowania tej ilości - zakładając, że 1 bajt danych to ziarenko ryżu, w 2020 roku ilość danych w ziarenkach ryżu wypełni cały Ocean Spokojny. Szkoda, że ten ryż nie rozwiąże problemu głodu na świecie… ale może chociaż się przyczyni do odnalezienia rozwiązania :) Tomek wspomniał o [3Vs](https://blog.sqlauthority.com/2013/10/02/big-data-what-is-big-data-3-vs-of-big-data-volume-velocity-and-variety-day-2-of-21/) - atrybutach/wymiarach opisujących Big Data. Internet nie śpi i w [sieci](http://www.klarity-analytics.com/2015/07/27/dimensions-of-big-data/) można znaleźć kolejne propozycje angielskich słów zaczynających się na V, które mogą posłużyć do określenia, z czym tak naprawdę mamy do czynienia. Po określeniu przestrzeni, w której będziemy się poruszać, Tomek w skrócie omówił język U-SQL (skrót skrótu - połączenie możliwości SQLa i C#), który zaraz po tym pokazał nam w praktyce. Korzystając z Visual Studio zaprezentował skrypty analizujące logi (po prostu kolejna analiza tekstu) oraz skrypty przetwarzające obrazy z wykorzystaniem modułów opatrzonych słówkiem [Cognitive](https://azure.microsoft.com/en-us/services/cognitive-services/). Za pomocą Cognitive-rzeczy możemy analizować obrazy - wyszukiwać na nich obiekty, osoby o określonej płci, wieku, śmiejące się, smutne. Nie musimy przy tym posiadać zaawansowanej wiedzy na temat przetwarzania obrazów. Dostępne moduły “przemielą” dane wejściowe za nas i “wyplują” wynik w postaci zbioru tagów opisującego obraz. To daje niekończące się możliwości.

##Podsumowanie
Obie prezentacje były na bardzo dobrym poziomie, a zaprezentowane zagadnienia były poruszone w ciekawy sposób i widać było, że obaj panowie znają się na rzeczy. Zakres materiału był całkiem fajnie wpasowany w okienka czasowe obu prelegentów. Zarówno Tomasz jak i Bartosz zaprezentowali ogólny zarys i skupili się później na smaczkach. Były też demo na żywo - kolejny raz mogliśmy zaobserwować, że najbardziej czasochłonnym procesem w obu przypadkach było “stawianie” środowiska :). Z kwestii organizacyjnych - catering pierwsza klasa, za to zdecydowanie musimy popracować nad gotowością do działania projektora w ProgressBarze.

##Jesteś ciekaw, co było na pierwszym spotkaniu? 
[Bartek](https://www.meetup.com/pl-PL/Microsoft-Azure-Users-Group-Poland/members/192982177/) wrzucił prezentacje na youtube’a:

* Krzysiek Szabelski [Rozproszona i asynchroniczna architektura oparta na Azure - case study z projektu](https://www.youtube.com/watch?v=mPfPM02uLJM)

* Stanisław Wawszczak [Wykorzystanie Azure Functions do zbierania danych z urządzeń pomiarowych](https://www.youtube.com/watch?v=YqyiwO8NAmw)

* Damian Mazurek [Od zera do IoT bohatera - czyli jak w prosty sposób przy wykorzystaniu Azurem zbudować własny system IoT](https://www.youtube.com/watch?v=WHW_Q2hbvi4)

Interesujesz się Azure i bywasz na Śląsku? Nie przegap kolejnych [spotkań](https://www.meetup.com/pl-PL/Microsoft-Azure-Users-Group-Poland/).
