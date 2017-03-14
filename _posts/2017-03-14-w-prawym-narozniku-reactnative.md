---
layout: post
title: W prawym narożniku - ReactNative
category: dajsiepoznac
comments: true
image: "/public/005-3 (Mobile).png"
date: 2017-03-14 21:15:00 0100
---
Gdzieś w sieci dostępny jest serwer z hubem signalR na pokładzie. Szczęśliwie się składa, że wiemy, gdzie dokładnie i w jaki sposób z owym hubem możemy “porozmawiać”. Czas stworzyć aplikację mobilną, która stanie się częścią naszej Domowej Biblioteki.

##Krok po kroku..
Podążając za [tutorialem](https://facebook.github.io/react-native/docs/tutorial.html) dostępnym na stronie ReactNative konfigurujemy środowisko. Na uwagę zasługuje fakt, że facebook sugeruje użycie narzędzia [Chocolatey](https://chocolatey.org/) - kto nie zna, niechaj się mu przyjrzy z bliska - całkiem wygodne i można sobie “zDevOpsować” konfigurację domowego sprzętu. Instalacja większości najczęściej używanych programów zaraz po formacie odpalając prosty skrypt? Brzmi kusząco…

Po udanej instalacji wszystkich niezbędnych elementów naszego środowiska możemy facebook sugeruje prostą komendę:

    react-native init HomeLibraryMobile

magia w konsoli i mamy gotową aplikację!

    react-native run-android 

wykonane w utworzonym katalogu z aplikacją skompiluje i uruchomi ją na podłączonym urządzeniu (emulatorze albo telefonie), a naszym oczom pojawi się prosty hello world. Czy da się zacząć prościej? Nie sądzę. Jak już jesteśmy w konsoli...

    code .

##Wygenerowana aplikacja
Przyjrzyjmy się bliżej potworkowi, który powstał za pomocą komendy init. Projekt jest wyraźnie podzielony na część dedykowaną Androidowi i iOSowi. Do rzeczy związanych z iOS zaglądał nie będę, póki co nie mam tam żadnego interesu, albo inaczej - wprowadzanie zmian w tym obszarze nie posiada wartości biznesowej.

<img class="postImage" src="/public/005-1 (Mobile).png" />

`android` -> Klik! Zaglądając do tego katalogu osoba posiadająca choć minimalne doświadczenie z programowaniem na platformę od Wujka Googla ujrzy… aplikację androidową! w katalogu app znajdziemy katalog `src`, w nim `main` z androidowym manifestem, gdzieś w otchłani katalogu `java` znajdą się `MainActivity.java` i `MainApplication.java`. Obie te klasy posiadają wiedzę o obiektach z React i Native w swoich nazwach. W tym momencie zostawmy te pliki w spokoju - bądźmy tylko świadomi ich istnienia. Nas interesują pliki z rozszerzeniem js.

<img class="postImage" src="/public/005-4.png" />

##ReactNative
Wracając do głównego katalogu natrafimy na 2 podobnie wyglądające pliki `index.android.js` oraz `index.ios.js` - one posłużą nam do rozwijania aplikacji pod konkretne platformy. Od nas zależy, ile kodu będzie wspólnego. Wartość biznesowa kieruje nas do pliku z androidem w nazwie. A w nim - nasz dobry znajomy, Reakcik! Klasa `HomeLibraryMobile` wita nas informacją, że sama już zdążyła rozszerzyć Component i ma dla nas wstępnie zaimplementowaną metodę `render`. Pojawiły się dziwne tagi htmlowe, rozpoczynające się z wielkiej litery. Web developerze znający Reacta - w tym momencie div został przemianowany na View! Spójrz jeszcze na sam dół tego pliku - rozpoznajesz CSSy? Skoro wszyscy się już znają, w gronie znajomych wprowadzenie pierwszej funkcjonalności będzie przyjemnością.

##Połączmy się z hubem
ReactNative pomimo swojego młodego wieku doczekał się już [szeregu paczek](https://react.parts/native) (bibliotek) tworzonych przez społeczność. Szczęśliwie się składa, że nie musimy kodzić komunikacji przez WebSockety, żeby skorzystać z signalR - z pomocą przyjdzie nam [react-native-signalr](https://github.com/olofd/react-native-signalr). Korzystając z instrukcji na githubie dorzucamy paczkę do naszego projektu, przeklejamy ze zrozumieniem kodzik inicjujący połączenie (wprowadzając po drodze kosmetyczne zmiany) i włączamy serwer.
<img class="postImage" src="/public/005-2 (Mobile).png" />
Może się zdarzyć, że nie będziemy w stanie połączyć się z naszym dev-środowiskiem hostowanym na IIS Express. Od czego mamy [stackoverflow](https://stackoverflow.com/questions/3313616/iis-express-enable-external-request/15809698#15809698). U mnie działa.

Na dzień dobry zawołajmy tę samą metodę huba, którą woła strona internetowa. Po drodze poinformujmy Użytkownika naszej aplikacji o stanie połączenia z serwerem wyświetlając [Toasta](https://facebook.github.io/react-native/docs/toastandroid.html).

<script src="https://gist.github.com/slawciu/d80b12decd59c4b14ef4eeaf6a28a65d.js"></script>

##Gdy coś pójdzie nie tak...
Co zrobić, gdy napisaliśmy dobry kodzik, ale jest jakiś błąd w jego wykonaniu i chcemy pokazać telefonowi, co robi źle… ReactNative w trybie debug uruchamia się na sporej nakładce z wbudowanymi potężnymi narzędziami. Jak się do niego dostać? Klikając przycisk menu, albo tak jak w moim przypadku - potrząsając telefonem. Polecam włączyć Hot Reloading (aplikacja przeładuje się, gdy zapiszemy edytowany plik w naszym IDE). W poszukiwaniu potencjalnych błędów pomoże nam debugger - opcja Debug JS Remotely odpali Chrome’a, a w konsoli developerskiej będziemy mieć możliwość debugowania kodu js naszej aplikacji - kolejny ukłon w stronę web-developerów.

<img class="postImage" src="/public/005-3 (Mobile).png" />

Ponadto wspomniana nakładka posiada bardzo przyjemny ekran błędów (czerwony) i ostrzeżeń (żółty). Gdy popełnimy jakiś błąd podczas bycia mobile developerem ReactNative podpowie co może być przyczyną błędu, a czasem nawet podpowie potencjalne rozwiązanie. Zupełnie nowa jakość po androidowym enigmatycznym "Wystąpił błąd, aplikacja została zamknięta" z podprogowym przekazem - miłego czytania logów, developerze!