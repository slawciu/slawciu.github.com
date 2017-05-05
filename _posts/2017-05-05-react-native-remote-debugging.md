---
layout: post
title: ReactNative Remote Debugging
category: dajsiepoznac
comments: true
image: "/public/020.gif"
date: 2017-05-05 08:52:00 0100
---

Rozwijanie aplikacji mobilnej wymaga połączenia między maszyną developerską a urządzeniem mobilnym. O ile w przypadku korzystania z emulatora to nie jest żaden problem - po prostu uruchamiamy kolejne okienko, to w przypadku fizycznych urządzeń sprawa zaczyna się delikatnie komplikować. Przywykłem do tego, że aby wgrać nową wersję aplikacji, musiałem podpinać telefon do komputera za pomocą kabelka USB.

ReactNative daje nam “opakowanie” wspomagające proces developmentu. Jego częścią jest menu, do którego możemy wejść przytrzymując przycisk menu na naszym telefonie lub potrząsając nim. Kiedy telefon jest podpięty kabelkiem, potrząsanie nie jest zbyt wygodne, a kabelek uderza o blat biurka - same problemy. Na szczęście istnieje rozwiązanie tego problemu. ReactNative chwali się tym, że w przypadku błędu, nie wyrzuca w kosmos całej aplikacji, tylko “dyskretnie” pokazuje, co poszło nie tak, prezentując biały tekst na czerwonym ekranie. Na jednym z takich ekranów możemy wyczytać, że w celu połączenia z serwerem developerskim należy fizycznie podpiąć telefon lub jeżeli z poziomu telefonu i komputera mamy dostęp do tej samej sieci - możemy podać adres IP serwera i port, pod którym serwer jest dostępny. Awesome!

<img class="postImage" src="/public/020.gif" />