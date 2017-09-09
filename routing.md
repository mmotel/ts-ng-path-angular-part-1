# Nawigacja

`Router` pozwala na nawigację pomiędzy widokami gdy użytkownik wykonuje akcje. 

![](/assets/routing.png)

## Podstawy

Aby móc skorzystać z `Router`-a należy dodać do aplikacji kilka elementów.

#### `<base href>`

Element ten wskazuje jak powinny być konstruowane adresy wewnątrz aplikacji. Musi on być pierwszym elementem w sekcji `<head>`.

Jeśli katalog `app` jest korzeniem całej aplikacji wtedy parametr `href` powinien być ustawiony tak:

```html
<base href="/">
```

#### `<router-outlet>`

Kolejnym istotnym elementem jest `<router-outlet>`. Wskazuje on `Router`-owi, w którym miejscu ma umieszczać zawartość widoków.

```html
<router-outlet></router-outlet>
```

#### konfiguracja

`Router` nie jest częścią `CoreModule`. Ma on swój własny moduł - `RouterModule`. należy go zaimportować.

```ts
import { RouterModule } from '@angular/router';
```

Kolejnym krokiem jest zdefiniowanie ścieżek. Ale o tym za chwilę.

#### nawigacja

Nawigacja jest możliwa na dwa sposoby.

Pierwszy z nich to skorzystanie z dyrektywy `RouterLink` dla elementu `<a>` lub `<button>`.

```html
<a [routerLink]="'/random'">Random</a>
```

Drugim jest skorzystanie z metod dostępnych w `RouterService`. 

```ts
this._router.navigateByUrl('/random');
```

## Definiowanie ścieżek

Aby zdefiniować ścieżkę należy zdefiniować obiekt typu `Routes`, który zawiera informacje, który komponent ma zostać załadowany pod wskazanym adresem. Dodatkowo możemy wskazać dodatkowe parametry oraz _strażników_ na wejście oraz wyjście z widoku.

```js
const appRoutes: Routes = [
  { path: 'random', component: RandomBeerComponent },
];
```

Przykład: `v17` [random-beer-routing.module.ts](https://github.com/mmotel/ng-beers-app/blob/v17/src/app/random-beer/random-beer-routing.module.ts).

## Parametry

Aby umieścić w adresie parametry należy skorzystać ze składni `:nazwaParametru`.

```js
const appRoutes: Routes = [
  { path: 'details/:id', component: BeerDetailsComponent },
];
```

Dostęp do parametrów z adresu zapewnia globalny serwis `ActivatedRoute` dostarczany przez `RouterModule`.

Najłatwiejszym sposobem jest skorzystanie z obiektu `snapshot`, który zawiera obecny stan aktywnej ścieżki w aplikacji - w tym obiekt `params` przechowujący parametry zawarte w adresie.

```ts
const beerId: number = +this._activatedRoute.snapshot.params['id'];
```

Przykład: `v17` [core-routing.module.ts](https://github.com/mmotel/ng-beers-app/blob/v17/src/app/core/core-routing.module.ts), [beer-details.component.ts](https://github.com/mmotel/ng-beers-app/blob/v17/src/app/core/beer-details/beer-details.component.ts).

Jednak jeśli nasz widok może nawigować sam do siebie zmieniając jedynie parametry w adresie wtedy konieczne będzie skorzystanie z mtody `ActivatedRoute.params`. Zwaraca ona `Observable` pozwalające reagować na zmiany parametrów widoku.

```ts
this._activatedRoute.params.subscribe( (params) => {
  const beerId: number = +params['id'];
});
```

## Parametry opcjonalne

Istnieje oczywiście możliwość dodawania parametrów opcjonalnych do ścieżek. Aby to zrobić należy przekazać do ścieżki obiekt zawierający parametry dodatkowe korzystając z notacji tablicowej.

```ts
this.additionalParams = {
  back: '/favourte'
};
```

```html
<a [routerLink]="['/details/', beer.id, additionalParams]">Details</a>
```

Aplikacja po zmianach `v18` ([github](https://github.com/mmotel/ng-beers-app/tree/v18/src/app)).

## Przekierowania

Mamy również możliwość przekierowania jednej ścieżki na drugą. Aby to zrobić należy zdefiniować ścieżkę w następujący sposób:

```ts
{path: '', redirectTo: '/list', pathMatch: 'full'}
```

Powyższa definicja mówi: przekieruj (dokładnie) ścieżkę `/` na `/list`.

Przykład: `v19` [app-routing.module.ts](https://github.com/mmotel/ng-beers-app/blob/v19/src/app/app-routing.module.ts), [core-routing.module.ts](https://github.com/mmotel/ng-beers-app/blob/v19/src/app/core/core-routing.module.ts).

## Lazy loading

Nasza aplikacja do uruchomienia potrzebuje załadować widoki listy oraz detali piwa. Większość użytkowników od razu trafia na jeden z tych widoków. Pozostałe mogą zostać przez nich nigdy nie odwiedzone. Pomimo tego są one ładowane od razu podczas startu aplikacji. Możemy to zmienić stosując leniwe ładowanie modułów.

![](/assets/lazy loading 2.png)

Aby załadować moduł leniwie należy zmodyfikować definicje ścieżek. 

```ts
// random-beer-routing.module.ts
const routes: Routes = [
  {path: '', component: RandomBeerComponent}
];

// app-routing.module.ts
const APP_ROUTES = [
  // ...
  { 
    path: 'favourite', 
    loadChildren: 'app/favourite/favourite.module#FavouriteModule' 
  },
  // ...
];

```


`- - -`

Przerobimy naszą aplikację tak aby ładowała `RandomBeerModule` oraz `FavouriteModule` dopiero kiedy użytkownik będzie chciał odwiedzić jeden z widoków, które one dostarczają.

Aplikacja po zmianach `v20` ([github](https://github.com/mmotel/ng-beers-app/tree/v20/src/app)).

---

###### Źródła

* https://angular.io/guide/router#routing--navigation