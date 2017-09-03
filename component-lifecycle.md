# Cykl życia komponentu

Komponenty (oraz dyrektywy) mają cykl życia, który jest zarządzany przez Angulara. 


![](/assets/lifecycle2.png)
`* niebieskie uchwyty są specyficzne dla komponentów`

> Angular creates it, renders it, creates and renders its children, checks it when its data-bound properties change, and destroys it before removing it from the DOM.

Aby podłączyć się do cyklu życia komponentu należy skorzystać z _"uchwytów"_, które są dostarczanie przez `CoreModule`. 

## OnInit

`ngOnInit` pozwala wykonać inicjalizację komponentu kiedy został on stworzony a jego parametry wejściowe zostały już ustawione. 

Najczęściej służy do pobierania parametrów ze ścieżki oraz komunikacji z serwerem.

## OnChanges

`ngOnChanges` pozwala na reakcję kiedy zmieniają się parametry wejściowe. 

Najczęściej jest miejscem, w którym następuje przeliczenie danych wyświetlanych przez komponent.

W specyficznych przypadkach `ngOnChanges` może całkowicie zastąpić `ngOninit`.

## AfterViewInit

`ngOnChanges` pozwala na wykonanie wykonanie akcji kiedy widok został już wyświetlony.

Bardzo przydatny szczególnie w przypadku dyrektyw kiedy potrzebujemy dostępu do już istniejącego elementu `DOM`.

## OnDestroy

`ngOnDestroy` służy do _"wyczyszczenia"_ komponentu zanim zostanie on usunięty z drzewa `DOM`. 

W tym miejscu zazwyczaj odpinamy dodatkowe `event listener`-y, kończymy działanie zewnętrznych bibliotek oraz przerywamy komunikację z serwerem jeśli Angular nie może zrobić tego sam. 

`- - -`

Przyjrzymy się bliżej `ngOnChanges`. Chcemy aby lista piw była posortowana alfabetycznie wedle nazw. Jednak chcemy sortowanie pzostawić w gestii komponentu wyświetlającego listę. 

`BeersListComponent` uwzględniający sortowanie ([github](https://github.com/mmotel/ng-beers-app/tree/v17/src/app/shared/beers-list)).

---

##### Źródła

* https://angular.io/guide/lifecycle-hooks#lifecycle-hooks