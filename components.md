# Komponenty

![](/assets/component.png)
`*` - `css` / `less` / `scss`
 
## Składowe komponentu

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

### template / templateUrl

### styles / stylesUrl

### providers

## Dzielenie na komponenty

## Interakcje między komponentami

### input

### output

### custom two-way binding