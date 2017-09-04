# Routing

`Router` pozwala na nawigację pomiędzy widokami gdy użytkownik wykonuje akcje. 

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

Przykład: [random-beer-routing.module.ts](https://github.com/mmotel/ng-beers-app/blob/v17/src/app/random-beer/random-beer-routing.module.ts).

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

Przykład: [core-routing.module.ts](https://github.com/mmotel/ng-beers-app/blob/v17/src/app/core/core-routing.module.ts), [beer-details.component.ts](https://github.com/mmotel/ng-beers-app/blob/v17/src/app/core/beer-details/beer-details.component.ts).

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

Aplikacja po zmianach ([github](https://github.com/mmotel/ng-beers-app/tree/v18/src/app)).

## Przekierowania

PRZYKŁAD: /random działa tylko raz, zrobić żeby działało cały czas

```js
const appRoutes: Routes = [
  { path: 'crisis-center', component: CrisisListComponent },
  { path: 'hero/:id',      component: HeroDetailComponent },
  {
    path: 'heroes',
    component: HeroListComponent,
    data: { title: 'Heroes List' }
  },
  { path: '',
    redirectTo: '/heroes',
    pathMatch: 'full'
  },
  { path: '**', component: PageNotFoundComponent }
];
```
 

## Lazy loading

PRZYKŁAD: zrobić lazy loading modułów random i favourite 

```js
{
  path: 'admin',
  loadChildren: 'app/admin/admin.module#AdminModule',
},
```

---

###### Źródła

* https://angular.io/guide/router#routing--navigation