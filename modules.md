# Moduły

Moduły pomagają podzielić aplikację na funkcjonalne części. 

`NgModule` to klasa udekorowana funkcją `@NgModule`. Przyjmuje ona metadane opisujące w jaki sposób należy zinterpretować i wykonać moduł oraz jego składniki.

```js
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

## CommonModule