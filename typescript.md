# TypeScript Notes
[Official Document](https://www.typescriptlang.org/)

## Interfaces
It is like blueprint.
[The explanation and examples.](https://www.tutorialsteacher.com/typescript/typescript-interface)


# RsJS Notes is also here


# Angular Notes
## Angular Concepts
[Official document](https://angular.io/guide/architecture) is great to read. But [the old type of this document](https://v2.angular.io/docs/ts/latest/guide/architecture.html) seems better to read

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
![data pass method](/images/data-pass-method.jpg)

## Injector of Service
![injector](https://angular.io/generated/images/guide/architecture/injector-injects.png)

![Injectable root and trees](https://2.bp.blogspot.com/-RJ8x9Ac5S8w/WEPqbAkwZxI/AAAAAAAAAN8/UibJElrG5n4QoihWnWRmRDPkgIFDIw5EwCK4B/s640/DependencyInjection1.png)

## Routing method
app-routing.modelu.ts defines what to show at <router-outlet></router-outlet>
```ts
const routes: Routes = [
  { path: "", redirectTo: "/dashboard", pathMatch: "full" },
  { path: 'heroes', component: HeroesComponent },
  { path: "dashboard", component: DashboardComponent },
  { path: "detail/:id", component: HeroDetailComponent }
];
```


