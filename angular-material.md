```
ng --version // Check the version and update
ng add @angualr/material // Add library to the project
ng g m material // Make the material forlder and material.module.ts
```
material.module.ts
```ts
import { NgModule } from '@angular/core';
import { MatSliderModule } from '@angular/material/slider';

const MaterialComponents = [
  MatSliderModule  // What you want to use
];

@NgModule({
  imports: [MaterialComponents],
  exports: [MaterialComponents]
})
export class MaterialModule { }
```

Then just import it inside app.module.ts
