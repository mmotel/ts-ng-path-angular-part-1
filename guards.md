# Strażnicy

W naszej aplikacji obecnie na każdy widok może wejść dowolny użytkownik. Podobnie sytuacja wygląda z opuszczaniem widoków. Można wyjść z nich mając niezapisane zmiany. 

W obu tych problemach z pomocą przychodzą nam strażnicy (_ang. guards_). Strażnik odpowiada za kontrolę możliwości wejścia oraz wyjścia z widoku. Można powiedzieć, że ustawiamy strażników na ścieżkach do oraz z widoku.

Implementacja strażnika powinna zwracać wartość `true` lub `false`. Może to zrobić synchronicznie lub asynchronicznie poprzez `Promise` czy też `Observable`. 

Gdy zwrócona zostanie wartość:
 * `true` - nawigacja będzie kontynuowana,
 * `false` - nawigacja zostanie zatrzymana i użytkownik pozostaje "na miejscu".

## canActivate

Prezentujemy piwa oraz ich szczegóły. Nie są to treści, które powinny być dostępne dla każdego - w szczególności dla osób niepełnoletnich. Przydałoby się zabezpieczyć widoki w naszej aplikacji przed nieuprawnionym dostępem.

Strażnik `canActivate` pozwala kontrolować możliwość załadowania widoku.

![](/assets/canActivate 3.png)

```ts
const routes: Routes = [
  {
    path: '', 
    component: RandomBeerComponent, 
    canActivate: [ IsAdultGuard ]
  }
];
```

Poza zwracaniem wartości `true/false` strażnik `canActivate` może też dokonać nawigacji, która spowoduje przerwanie nawigacji podobnie jak zwrócenie wartości `false`.

Aplikacja po zmianach `v21` ([github](https://github.com/mmotel/ng-beers-app/tree/v21/src/app)).

## canDeactivate

Nasza aplikacja zyskała nową funkcjonalność - możliwość dodawania komentarzy do piw na widoku detali piwa `v22` ([github](TODO)). Obecnie po dodaniu komentarza możemy opuścić widok bez zapisywania. Nie jest to najlepsze zachowanie z punktu widzenia użytkownika. Należy dodać zabezpieczenie przed opuszczeniem widoku bez zapisywania zmian.

Strażnik `canDeactivate` służy do kontrolowania możliwości opuszczenia widoku.

![](/assets/canDeactivate 2.png)

Przykłady: core-routing.module.ts, core/beer-details.module.ts, can-deactivate.guard.ts

PRZYKŁAD: `v23` dodawanie notatek do piw - pilnowanie wyjścia bez zapisu

---

###### Źródła

* https://angular.io/guide/router#milestone-5-route-guards