---
layout: post
title: To uczucie, kiedy możesz zobaczyć powietrze, którym oddychasz...
category: dajsiepoznac
tags: [elektronika, smogomierz, grafana, influxdb, iot]
comments: true
image: "/public/023/04.png"
date: 2018-11-16 22:00:00 0100
---
Co można dostać na urodziny? A co można dostać jeśli to są duże urodziny i otwiera się wiele możliwości? Jak jest się nudnym człowiekiem chcącym dbać o swoje zdrowie można dostać oczyszczacz powietrza! Zwłaszcza, że są momenty w roku, gdzie widok za oknem może zmusić do refleksji...

<img class="postImage" style="width: 100%" src="/public/023/04.png" />

Tak oto w naszym mieszkaniu pojawił się oczyszczacz powietrza Sharp, którego testy pojawiły się na [Spider's Web](https://www.spidersweb.pl/2017/03/sharp-kc-a50euw-opinie-recenzja.html) - artykuł mocno przyczynił się do wyboru akurat tego modelu. Z tym oczyszczaczem żyjemy już prawie rok, przez cały ten czas łudząc się, że nasze powietrze jest lepsze. W tym miejcu historii pojawiają się internety, konkretnie facebook. Na rzeczonym facebooku pojawiają się różne rzeczy, zwłaszcza gdy się pomoże trochę szczęściu i algorytmom, klikajac Lubię to dla [TEDxKatowice](https://www.facebook.com/tedxkatowice/) i [HackerSpace Silesia](https://www.facebook.com/HackerspaceSilesia/). Tak oto wydarzenie “zbuduj sobie smogomierz” objawiło przede mną tajemne sekrety: gdzie i kiedy.

##Smogomierze
W okolicy można znaleźć wiele czujników zanieczyszczeń, rozmieszczonych w różnych miejscach w mieście. Jakość powietrza zależy od wielu czynników - otoczenia domów jednorodzinnych, ruchliwych dróg w okolicy, ukształtowania terenu albo urbanisty, który nie pozwoli na wybudowanie kilkunastopiętrowego budynku w tzw. korytarzu powietrznym miasta. Żaden z okolicznych czujników nie wzbudzał w nas zaufania na tyle, by choćby przez chwilę nie myśleć o złożeniu własnego (mieszkamy trochę dalej i wyżej, niż domy jednorodzinne, przy których zamontowany jest najbliższy czujnik). Dlatego nim się obejrzeliśmy, siedzieliśmy w siedzibie HackerSpace Silesia w Katowicach, z elektroniką gotową do rozpakowania.

Event był mocno związany z niemiecką inicjatywą o polskich korzeniach - [luftdaten.info](https://luftdaten.info/). Jak się okazało, jest to [open source’owy](https://github.com/opendata-stuttgart) projekt zapoczątkowany przez Lucasa, a właściwie Łukasza, który swego czasu wyemigrował za zachodnią granicę i na jednym z eventów typu Code for Germany stworzył zalążki systemu, którego czujniki pokrywają prawie całe Niemcy i coraz częściej pojawiają się w innych krajach - patrz [mapa](http://deutschland.maps.luftdaten.info/#6/51.165/10.455).

W skład smogomierza wchodzą: 

 * mikrokontoler NodeMCU ESP8266 v3
 * czujnik pyłu SDS011
 * czujnik temperatury i wilgotności DHT22
 * zasilacz 5V/2.1A (mam nadzieję, że nie jest na czarnej liście na elektrodzie…)
 * przewód microUSB
 * kabelki!

##SDS011 i DHT22
SDS011 ([datasheet](https://nettigo.pl/attachments/398)) to czujnik wykorzystujący lasery do pomiaru stężenia cząstek w badanym powietrzu. Badanie polega na zaciągnięciu powietrza do wnętrza czujnika (pomaga tu mały wentylator) i pomiar za pomocą lasera. Warto w tym momencie wspomnieć o niedoskonałości tego rozwiązania - kiedy wzrasta wilgotność, cząsteczki wody mogą być rozpoznane jako cząsteczki pyłu, co może negatywnie wpływać na odczyt. Dlatego wspomagamy się jeszcze DHT22 ([datasheet](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)) - czujnikiem, który mierząc temperaturę i wilgotność, pozwoli nam wprowadzać korekty do odczytów czujnika pyłu.

<img class="postImage" style="width: 75%" src="/public/023/03.png" />

Producent czujnika pyłu gwarantuje prawidłowe odczyty przez około rok ciągłej pracy. By móc korzystać z czujnika dłużej, niż rok, potraktujemy go trochę tak, [jak powinno się traktować LEDy](http://rzeczybezinternetu.blogspot.com/2016/03/wyjscie-blink-world.html) - będziemy go załączać co jakiś czas. Dzięki temu rozciągniemy w czasie nasz rok ciągłej pracy. Nie potrzebujemy pomiarów w czasie rzeczywistym, w zupełności zadowolimy się odczytami co kilkudziesiąt sekund. 

Samo składanie polegało na podłączeniu odpowiednich pinów czujników do pinów wyprowadzonych na płytce z czujnikiem. Dostarczony był też skompilowany kodzik, który wystarczyło wrzucić na procka, jak tylko system zaczął go wykrywać pod którymś portem COM. Na sam koniec pozostała konfiguracja. I najciekawsze - gdzie można te dane zobaczyć/wysłać?!

Aplikacja od luftdaten stawia na ESP serwer www, za pomocą którego mamy dostęp do ostatniego odczytu i szeregu ustawień konfiguracyjnych. 
<img class="postImage" src="/public/023/02.png" />

Zaznaczając w konfiguracji checkbox "Wysyłaj tam Feinstaub-App" jesteśmy w stanie podglądać odczyty czujnika także za pomocą aplikacji mnobilnej [Particulate Matter App](https://play.google.com/store/apps/details?id=com.mrgames13.jimdo.feinstaubapp). Uwagę zwracają miejsce na link do zewnętrznego API i pola konfiguracyjne dla serwera bazy InfluxDB.
Wrodzona ciekawość, co się wysyła sprawiła, że po paru minutach stał json-server. Hint - w adresie serwera nie podawać http. Z czujnika przyszedł piękny json:

```
{
      "esp8266id": "760xxxx",
      "software_version": "NRZ-2018-111",
      "sensordatavalues": [
        {
          "value_type": "SDS_P1",
          "value": "51.80"
        },
        {
          "value_type": "SDS_P2",
          "value": "28.10"
        },
        {
          "value_type": "temperature",
          "value": "21.80"
        },
        {
          "value_type": "humidity",
          "value": "56.20"
        },
        {
          "value_type": "samples",
          "value": "602632"
        },
        {
          "value_type": "min_micro",
          "value": "229"
        },
        {
          "value_type": "max_micro",
          "value": "2457095"
        },
        {
          "value_type": "signal",
          "value": "-72"
        }
      ],
      "id": 2
    }
```

No to teraz wykres! I proces myślowy: trzeba postawić api, gdzieś serwer, potem UI, pewnie React, pewnie d3js… Czy nie da się prościej?

##Grafana i InfluxDB
Podczas samego eventu, [Błażej](https://github.com/bfaliszek) pokazał swój dashboard skonfigurowany w Grafanie, na którym prezentuje odczyty z własnych czujników. Odrobina googlowania z słowami kluczowymi “Grafana InfluxDB” doprowadziła do tego, że nim się obejrzałem miałem już prywatne konto na Grafanie i szukałem miejsca na hosting bazy. Tu z pomocą przyszła maszyna wirtualna hostowana na Azure, z Ubuntu na pokładzie. 2 komendy - jedna instalacyjna, druga uruchamiająca serwer w tle, umożliwiły utworzenie nowej bazy danych i użytkowników - dla sensorów i grafany. InfluxDB jest jednym z dostępnych źródeł danych w samej Grafanie. Po dodaniu namiarów na serwer, użytkownika, można testować połączenie i przekonać się, że… trzeba jeszcze otworzyć port na Azure i wtedy - wszystko bangla.

##Dashboard
Jeszcze tylko wytłumaczyć Grafanie, co chciałbym zobaczyć - wykres stężenia pyłu PM2.5 i pyłu PM10. Z czujnika jeszcze otrzymujemy informację o wilgotności i temperaturze - te dane też wylądują na ekranie. Fajnym pomysłem było też naniesienie europejskich norm jakości powietrza - stąd threshold w postaci czerwonej linii.

<img class="postImage" style="width: 100%" src="/public/023/01.png" />