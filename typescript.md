# TypeScript Notes
[Official Document](https://www.typescriptlang.org/)

## Interfaces
It is like blueprint.
[The explanation and examples.](https://www.tutorialsteacher.com/typescript/typescript-interface)


# RsJS Notes is also here


# Angular Notes

## pipes
Angular built in functions, see [official document](https://angular.io/guide/pipes)

## Data binding: ngModel, css class binding, click method, ...
```html
<li *ngFor="let hero of heroes"
  [class.selected]="hero === selectedHero"
  (click)="onSelect(hero)">
  <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>
<input [(ngModel)]="selectedHero.name" placeholder="name" />
```

## Data passes to another component
!(data pass method)[./images/data-pass-method.jpeg]
