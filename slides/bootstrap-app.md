### Bootstrap Angular Web App
<!-- .slide: data-background="img/background-orange-orig.jpg" -->

Angular is now platform and can be used in different environments. 
In this case we will explicitly define that we will use Angular app in browser.

```
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from 
    '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule);
```

---

### Defining module
<!-- .slide: data-background="img/background-orange-orig.jpg" -->

```
@NgModule({
  declarations: [
    AppComponent,
    HelloWorldComponent,
    UserItemComponent,
    UserListComponent
], imports: [ 
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
}) 
export class AppModule { } 
```

Note:
Show examples from application