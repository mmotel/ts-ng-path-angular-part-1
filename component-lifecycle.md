# Cykl życia komponentu

Komponenty (oraz dyrektywy) mają cykl życia, który jest zarządzany przez Angulara. 


![](/assets/lifecycle2.png)
`* niebieskie uchwyty są specyficzne dla komponentów`

> Angular creates it, renders it, creates and renders its children, checks it when its data-bound properties change, and destroys it before removing it from the DOM.

Aby podłączyć się do cyklu życia komponentu należy skorzystać z _"uchwytów"_, które są dostarczanie przez `CoreModule`. 

## OnInit

`ngOnInit` pozwala wykonać inicjalizację komponentu kiedy został on stworzony a jego parametry wejściowe zostały już ustawione. 

Najczęściej służy do pobierania parametrów ze ścieżki oraz komunikacji z `api`.

## OnChanges

`ngOnChanges` pozwala na reakcję kiedy zmieniają się parametry wejściowe. 

Najczęściej jest miejscem, w którym następuje przeliczenie danych wyświetlanych przez komponent.

W specyficznych przypadkach `ngOnChanges` może całkowicie zastąpić `ngOninit`.

## AfterViewInit



## OnDestroy