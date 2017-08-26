# Komponenty

Komponent kontroluje fragment ekranu zwany widokiem. Składa się z trzech podstawowych elementów - logiki, szablonu oraz styli.

![](/assets/component.png)  
`*` - `css` / `less` / `scss`

## Składowe komponentu

`Component` to klasa udekorowana funkcją `@Component`. Przyjmuje ona metadane opisujące w jaki sposób należy zinterpretować i wyświetlić komponent oraz czego potrzebuje on do działania.

```ts
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

Przyjrzyjmy się komponentowi `BeerDetailsComponent` \([github](https://github.com/mmotel/ng-beers-app/tree/v4/src/app/core/beer-details)\).

## Dzielenie na komponenty

Kiedy nasza aplikacja zaczyna się rozrastać pojawiają się miejsca gdzie powtarzają się elementy interfejsu. Warto w takich wypadkach uniknąć redundancji kodu i stworzyć reużywalny komponent.

![](/assets/spliting view into components.png)

W naszym przypadku takim komponentem będzie karta z detalami pojedynczego piwa.

Wydzielimy nasz komponent i wykorzystamy go na widokach detali piwa oraz nowym pokazującym losowe piwo.

Aplikacja po wydzieleniu i wykorzystaniu `BeerCardComponent` ([github](https://github.com/mmotel/ng-beers-app/tree/v6/src/app)).

## Interakcje między komponentami

Podział widoków na komponenty i umieszczanie ich w sobie sprawia iż konieczna staje się komunikacja pomiędzy komponentami.

![](/assets/component interactions part 1.png)

### input

Pole komponentu udekorowane funkcją `@Input()` pozwala na przekazanie do niego wartości przez rodzica przy użyciu kwadratowych nawiasów `[ ]`.

### output

Pole komponentu udekorowane funkcją `@Output()` pozwala na przekazanie wartości do rodzica przy użyciu okrągłych nawiasów `( )`. Pole to musi być typu [`EventEmitter<T>`](https://angular.io/api/core/EventEmitter).

### custom two-way binding

Łącząc ze sobą parę `input` - `output` możemy stworzyć własny `two-way binding` - działający tak jak `[(ngModel)]`. Ważną kwestią są w tym przypadku nazwy pól. Pole `output` musi mieć nazwę składającą się z nazwy pola `input` oraz sufiksu `Change`.

```ts
@Input() value: string;
@Output() valueChange: EventEmitter<string> = new EventEmitter<string>();
```

### @ViewChild

Dekorator `@ViewChild` pozwala uzyskać _uchwyt_ do komponentu dziecka. Dzięki temu możemy wywołać jego publiczne metody oraz zyskujemy dostęp do publicznych pól.

```ts
@ViewChild(BeerCardComponent) private beerCard: BeerCardComponent;
```

### ng-content

## Dwa rodzaje komponentów

Widok vs reużywalny komponent



