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

```js
const appRoutes: Routes = [
  { path: 'crisis-center', component: CrisisListComponent },
];
```


## Parametry

```js
const appRoutes: Routes = [
  { path: 'crisis-center', component: CrisisListComponent },
  { path: 'hero/:id',      component: HeroDetailComponent },
];
```

## Parametry opcjonalne / dodatkowe

## Przekierowania

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

```js
{
  path: 'admin',
  loadChildren: 'app/admin/admin.module#AdminModule',
},
```

---

###### Źródła

* https://angular.io/guide/router#routing--navigation