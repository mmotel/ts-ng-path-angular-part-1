# Moduły

Moduły pomagają podzielić aplikację na funkcjonalne części. 

![](/assets/app modules structure.png)

`NgModule` to klasa udekorowana funkcją `@NgModule`. Przyjmuje ona metadane opisujące w jaki sposób należy zinterpretować i wykonać moduł oraz jego składniki.

```ts
@NgModule({
  imports:      [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ],
  exports:      [],
  providers:    []
})
export class AppModule { }
```

## Składowe modułu

Metadane opisujące moduł składają się z czterech tablic.

### `declarations`

Tablica `declarations` definiuje składniki definiowanego modułu. Mogą nimi być komponenty, dyrektywy oraz potoki. Każdy komponent musi należeć do jednego modułu.

### `imports`

Tablica `imports` zawiera moduły, które zostaną zaimportowane do modułu. Składniki tych modułów będą dostępne dla wszystkich składników definiowanego modułu.

### `exports`

`exports` pozwala na udostępnienie wybranych składników modułu innym, które go zaimportują.

### `providers`

`providers` definiuje serwisy, które zostaną dostarczone do komponentów wewnątrz definiowanego modułu oraz tych modułów, które go zaimportują. 

### `bootstrap`

`bootstrap` wskazuje komponent, który jest punktem wejściowym aplikacji. Właściwość tą może zawierać tylko jeden moduł w aplikacji - główny, zazwyczaj nazywany `AppModule`. 

## RootModule

Moduł główny aplikacji - zazwyczaj nazywany `AppModule` pełni rolę punktu startowego. Jego głównym zadaniem jest definiowane struktury aplikacji poprzez importy oraz routing.

Przyjrzyjmy się temu jak obecnie wygląda nasza aplikacja ([github](https://github.com/mmotel/ng-beers-app/tree/v0/src/app)). 

## CoreModule

`CoreModule` zawiera w sobie podstawowe elementy aplikacji, które zawsze są ładowane podczas jej uruchamiania. 

Wydzielimy do `CoreModule` elementy, które obecnie znajdują się w `AppModule` aby mógł on pełnić swoją podstawową rolę.

Aplikacja po wydzieleniu `CoreModule` ([github](https://github.com/mmotel/ng-beers-app/tree/v1/src/app)).

## SharedModule

`SharedModule` przechowuje w sobie elementy aplikacji, które są współdzielone przez jej moduły. Dodatkowo importuje i eksportuje moduły, które musielibyśmy importować w wielu miejscach.

Aplikacja po wydzieleniu `SharedModule` ([github](https://github.com/mmotel/ng-beers-app/tree/v2/src/app)).

Warto również uporządkować elementy współdzielonego modułu. Obecnie wiele z nich powtarza się w tablicach `imports` / `declarations` i `exports`. Pogrupujemy elementy wedle typów do tablic, które następnie wykorzystamy w `imports`, `declatarions` oraz `exports`.

`SharedModule` po uporządkowaniu ([github](https://github.com/mmotel/ng-beers-app/blob/v3/src/app/common/common.module.ts)).

## FeatureModule

`FeatureModule` zawiera niezależną część aplikacji - pojedynczą funkcjonalność. Moduły te są zazwyczaj ładowane na żądanie (`lazy loading`) kiedy są potrzebne. W ich kontekście bardzo istotny staje się `SharedModule` ponieważ nie powinny one importować siebie na wzajem a jedynie korzystać ze współdzielonego modułu.

Wraz z rozwojem aplikacji rośne liczba jej funkcjonalności. Natychmiastowe ładowanie wszystkich jej części jest niewydajne i wydłuża czas oczekiwania na uruchomienie aplikacji. Podział na `FeatureModules` pozwala na doładowywanie kolejnych funkcjonalności w razie potrzeby gdy użytkownik będzie chciał z nich skorzystać.

Stworzymy `FeatureModule`, który będzie zawierał funkcjonalność wyświetlania detali losowego piwa.

Nasz now moduł - `RandomBeerModule` ([github](https://github.com/mmotel/ng-beers-app/tree/v4/src/app/random-beer)).


---

##### Źródła

* https://angular.io/guide/bootstrapping
* https://angular.io/guide/ngmodule