# Strażnicy (Guards)

W naszej aplikacji obecnie na każdy widok może wejść dowolny użytkownik. Podobnie sytuacja wygląda z opuszczaniem widoków. Można wyjść z widoków mając niezapisane zmiany. 

W obu tych problemach z pomocą przychodzą nam strażnicy (_ang. guards_). Strażnik odpowiada za kontrolę możliwości wejścia oraz wyjścia z widoku. Można powiedzieć, że ustawiamy strażników na ścieżkach do oraz z widoku.

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

PRZYKŁAD: pilnowanie czy osoba jest pełnoletnia

## canDeactivate

![](/assets/canDeactivate 2.png)

PRZYKŁAD: dodawanie notatek do piw - pilnowanie wyjścia bez zapisu