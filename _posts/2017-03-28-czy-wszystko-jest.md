---
layout: post
title: Czy wszystko jest?
category: dajsiepoznac
comments: true
date: 2017-03-28 21:00:00 0100
image: '/public/009.png'
---

Testować możemy wszystkie składowe Reduxa. Wiemy już jak ugryźć Reducers. Teraz czas na Components i Actions.

##Components
<script src="https://gist.github.com/slawciu/1c3c69605ba2feca771e923f57f4a068.js"></script>
W celu sprawdzenia, czy nasz komponent jest w stanie się prawidłowo narysować (wyrenderować) musimy go przesłać jako parametr metody create() renderera z paczki [react-test-renderer](https://www.npmjs.com/package/react-test-renderer). Przesłanie Reacta jest proste - możesz mnie użyć wszędzie, gdzie dostępny będzie odpowiedni renderer (nawet na bardzo niskim poziomie, patrz [ReactHardware](https://github.com/iamdustan/react-hardware). I proszę bardzo - chcę uruchomić Reacta w testach, więc wykorzystuję renderera :) Obiekt zwrócony przez metodę create w moim przypadku wygląda tak:
<script src="https://gist.github.com/slawciu/fca16ef13a23d921cdbc2157a3f57bce.js"></script>
Odpowiada temu, co wcześniej zakodziłem w BooksList. Operując na tym jsonie jesteśmy w stanie sprawdzać, czy poszczególne elementy naszego widoku są widoczne, czy nie. Gwoli wyjaśnienia - w celu zapewnienia wykonania testu, musiałem dorzucić kilka propsów: store, navigator i route - podobnie jak w użyciu tego komponentu w testowanej aplikacji. Ten test potraktuję jako smoke’a i nic dodatkowo nie sprawdzę.

##Actions
A właściwie ActionsCreators zwracają obiekt akcji, która ma wpłynąć na stan aplikacji. 
<script src="https://gist.github.com/slawciu/0998807fd96b7405c251aaadf6406b84.js"></script>

Podobnie jak w przypadku Reducera - odpalamy metodę i sprawdzamy, czy otrzymany obiekt odpowiada oczekiwanemu.

##\_\_mocks\_\_
Prędzej czy później - musiały się pojawić. Aplikacja mobilna wykorzystuje signalR, a w testach opieranie się na tym, że gdzieś w cyberprzestrzeni jest uruchomiony jakiś hub, który może wpłynąć na wyniki naszych testów jest... niebezpieczne, niepoważne - jednym słowem - nie. Wykorzystując mechanizm mockowania dostarczony przez jest skrobniemy na szybko mocka signalRa.

SignalR to nie jedyna przeszkoda w testowaniu. Może się zdarzyć, że testowane przez nas komponenty będą korzystać z zewnętrznych zależności - w moim przypadku kontrolki stylu. Na chwilę obecną nie są mi potrzebne, dla nich mock też powstanie. Jedyny zgrzyt, jaki się tu pojawia, to konieczność tworzenia katalogu \_\_mocks\_\_ jak najbliżej mockowanej paczki/biblioteki. I tak dla klienta signalr, który wylądował w katalogu lib, mock musiał sie znaleźć w lib\\\_\_mocks\_\_, a mock dla material ui zasłużył na katalog 'obok' node_modules. Osobiście nie podoba mi się takie podejście, gdyż logika testów jest rozsmarowana po całym repo - z drugiej strony mocki mamy najbliżej mockowanej funkcjonalności jak się tylko da. Całe szczęście, że Visual Studio 'skraca' nam drogę między testem a implementacją rozsądną nawigacją.

<img class="postImage" src="/public/009.png" />

Zielono!