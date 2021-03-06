---
layout: post
title: W lewym narożniku - React i SignalR...
category: dajsiepoznac
comments: true
date: 2017-03-08T21:15:00+01:00
image: "/public/003.png"
---

W ramach konkursu Daj się poznać rozwijam aplikację do zarządzania domowym zbiorem książek. Na [githubie](https://github.com/slawciu/home-library) wylądował pierwszy kawałek kodu.

<img class="postImage" src="/public/003.png" />

## SignalR
Biblioteka dostarczana przez Microsoft, jak sami się chwalą:
"Incredibly simple real-time web for .NET"
i mają rację. Po stronie serwera musimy zakodzić Hub, po stronie klienta połączyć się do tego Huba. Biblioteka sprawi, że w aplikacji będziemy mieć dostępne “stałe łącze” między klientami a serwerem. W pudełku z samym signalR dostajemy informację o połączonych klientach (po stronie Huba), z możliwością filtrowania odbiorców potencjalnych wiadomości. 
Jak wygląda komunikacja? Posiadając nawiązane połączenie, po stronie klienta wywołujemy metodę dostępną w hubie:

    $.connection.hub.url = "/signalr";
    this.sHub = $.connection.library;

    this.sHub.client.updateLibraryState = function (libraryState) {
        this.setState((prevState, props) => {
                return { libraryState: libraryState }
        });
    }.bind(this);

    $.connection.hub.start().done(function () {
        this.sHub.server.getLibraryState("Maurice");
    }.bind(this));

Jeżeli klient, który wywołał funkcję huba ma zaimplementowaną obsługę metody updateLibraryState, będzie w stanie zareagować na “głos serwera”. Zwróć uwagę, że hub posiada informację o bycie, który wykonał na nim metodę.
    
    public void GetLibraryState(string myIdentity)
    {
        Clients.Caller.updateLibraryState($"new state for you, {myIdentity}");
    }

#React
Kiedy Facebook [poinformował świat](https://www.youtube.com/watch?v=XxVg_s8xAms) o swoim najmłodszym dziecku - React - wszyscy pukali się w głowę. W świecie web-developmentu, gdzie rozłączność czystego htmla, javascriptu i cssów jest świętością, pojawili się goście od Marka Z. i próbują przekonać całe to świątobliwe towarzystwo, że wrzucenie htmla do javascriptu to będzie przełom. I przełom nastąpił. Statyczny html wykorzystujemy do tworzenia komponentów, które mają swój stan - state i niezmienniki - props. Zmiana stanu powoduje, że komponent jest przerysowany - tj coś zmienia się w oknie przeglądarki użytkownika. Co jest najbardziej sexy w tym całym “reakcie”? [Algorytm](https://facebook.github.io/react/docs/reconciliation.html), który sprawia, że przerysowują się tylko te komponenty, których stan uległ zmianie. Jak wygląda ten potworek od FB?

    render() {
        return (<div>
                    <h1>Domowa Biblioteka</h1>
                    <div>Gdzieś poniżej wyświetlimy książki...</div>
                    <div>Stan biblioteki: { this.state.libraryState }</div>
                </div>);
    }

Każdemu komponentowi musimy powiedzieć, jak się ma narysować (implementując funkcję render) tu możemy stworzyć potworka htmlowo-javascriptowego. Oprócz tego, do dyspozycji mamy kilka “wejść” w czas życia komponentu:

* [componentWillMount()](https://facebook.github.io/react/docs/react-component.html#componentwillmount)
* [componentDidMount()](https://facebook.github.io/react/docs/react-component.html#componentdidmount)
* [componentWillReceiveProps()](https://facebook.github.io/react/docs/react-component.html#componentwillreceiveprops)
* [componentWillUpdate()](https://facebook.github.io/react/docs/react-component.html#componentwillupdate)
* [componentDidUpdate()](https://facebook.github.io/react/docs/react-component.html#componentdidupdate)
* [componentWillUnmount()](https://facebook.github.io/react/docs/react-component.html#componentwillunmount)

Przy okazji polecam dokumentację od FB - daje radę. Moja biblioteka skorzysta z łącznika między czystym Reactem a światem .NETa - [ReactJS.net](https://reactjs.net/)

## Kodzik
Co robi kodzik? Po uruchomieniu, z poziomu komponentu Dashboard wołana jest metoda huba library - żądanie o aktualny stan biblioteki, opatrzone prostym parametrem. Hub w podzięce za pobudzenie, wywołuje metodę klienta, który go zawołał, a otrzymana wiadomość pojawia się na stronie. Ta skomplikowana machina ma swoje miejsce w chmurze Azure.