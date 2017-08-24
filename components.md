# Komponenty

Komponent kontroluje fragment ekranu zwany widokiem. Składa się z trzech podstawowych elementów - logiki, szablonu oraz styli.

![](/assets/component.png)
`*` - `css` / `less` / `scss`
 
## Składowe komponentu

`Component` to klasa udekorowana funkcją `@Component`. Przyjmuje ona metadane opisujące w jaki sposób należy zinterpretować i wyświetlić komponent oraz czego potrzebuje on do działania.

```js
@Component({
  selector: 'app-loading',
  styleUrls: ['./loading.component.css'],
  template: `<md-spinner></md-spinner>`,
  providers: []
})
export class LoadingComponent {}
```

### selector

Selektor definiuje element HTML, który zostanie wypełniony przez zawartość komponentu. W przypadku komponentów, które są wykorzystywane w routingu parametr `selector` może zostać pominięty.

### template / templateUrl

Szablon komponentu można zdefiniować na dwa sposoby. Liniowo - umieszczając go w tym jednym pliku z logiką - wykorzystując parametr `template`. Drugą możliwością jest umieszczenie szablonu w oddzielnym pliku - służy do tego parametr `templateUrl`. 

### styles / stylesUrl

Podobnie jak szablon tak i style możemy zdefiniować zarówno liniowo jak i w osobnym pliku. Różnica polega na możliwości użycia wielu plików ze stylami. Style komponentu są domyślnie ograniczone tylko do jego elementów.

Definiując style komponentu mamy do dyspozycji dwa specjalne pseudoelementy - `:host` oraz `:host-context()`. 

`:host` pozwala się odwołać do elementu okalającego zawartość komponentu - nazywa się on tak jak selektor, o ile został zdefiniowany.

`:host-context(.class-name)` pozwala odwołać się do kontekstu elementu okalającego zawartość komponentu i sprawdzić czy na przykład na on nadaną klasę `class-name`.

### providers

Tablica `providers` definiuje serwisy, które zostaną dostarczone do komponentu podczas jego tworzenia.  

`- - -`

Przyjrzyjmy się komponentowi `BeerDetailsComponent` ([github](https://github.com/mmotel/ng-beers-app/tree/v4/src/app/core/beer-details)).

## Dzielenie na komponenty

## Interakcje między komponentami

### input

### output

### custom two-way binding