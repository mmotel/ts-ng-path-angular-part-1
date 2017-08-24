# Komponenty

Komponent kontroluje fragment ekranu zwany widokiem. Składa się z trzech podstawowych elementów - logiki, szablonu oraz styli.

![](/assets/component.png)
`*` - `css` / `less` / `scss`
 
## Składowe komponentu

`Component` to klasa udekorowana funkcją `@Component`. Przyjmuje ona metadane opisujące w jaki sposób należy zinterpretować i wyświetlić komponent oraz czego potrzebuje on do działania.

```js
@Component({
  selector: 'hero-app',
  template: `
    <h1>Tour of Heroes</h1>
    <hero-app-main [hero]=hero></hero-app-main>`,
  styles: ['h1 { font-weight: normal; }'],
  providers: []
})
export class HeroAppComponent {
/* . . . */
}
```

### selector

Selektor definiuje element HTML, który zostanie wypełniony przez zawartość komponentu. W przypadku komponentów, które są wykorzystywane w routingu parametr `selector` może zostać pominięty.

### template / templateUrl

Szablon komponentu można zdefiniować na dwa sposoby. Liniowo - umieszczając go w tym jednym pliku z logiką - wykorzystując parametr `template`. Drugą możliwością jest umieszczenie szablonu w oddzielnym pliku - służy do tego parametr `templateUrl`. 

### styles / stylesUrl

Podobnie jak szablon tak i style możemy zdefiniować zarówno liniowo jak i w osobnym pliku. Różnica polega na możliwości użycia wielu plików ze stylami. Style komponentu są domy

### providers

## Dzielenie na komponenty

## Interakcje między komponentami

### input

### output

### custom two-way binding