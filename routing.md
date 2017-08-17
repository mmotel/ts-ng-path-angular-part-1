# Routing

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

