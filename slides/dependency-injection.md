### Dependency injection
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->

When module A requires module B to run, we say that B is a dependency of A. 

- substitute out the implementation of B for MockB during testing
- share a single instance of the B class across our whole app (e.g. the Singleton pattern)
- create a new instance of the B class every time it is used (e.g. the Factory pattern)

The major benefit of using Dependency Injection is that the client component needn’t be aware of to create the dependencies. 
All the client component needs to know is how to interact with those dependencies.

Note: 
Dependency Injection can solve these problems. 
Dependency Injection (DI) is a system to make parts of our program accessible to other parts of the program - and we can configure how that happens. 
One way to think about “the injector” is as a replacement for the new operator. That is, instead of using the language-provided new operator, Dependency Injection let’s us configure how objects are created. 
The term Dependency Injection is used to describe both a design pattern (used in many different frameworks) and also the specific implementation of DI that is built-in to Angular. 

---

### Init Service without DI
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->

```
import { PriceService } from './price.service';
export class Product { 
    service: PriceService; basePrice: number;
    constructor(basePrice: number) {
        this.service = new PriceService(); // <-- create directly ("hardcoded") this.basePrice = basePrice;
    }
    totalPrice(state: string) {
        return this.service.calculateTotalPrice(this.basePrice, state);
    } 
}
```

```
import { Product } from './product';
describe('Product', () => {
    let product;
  beforeEach(() => {
    product = new Product(11);
  });
  describe('price', () => {
    it('is calculated based on the basePrice and the state', () => {
      expect(product.totalPrice('FL')).toBe(11.66); // <-- hmmm
    });
  }) 
});
```
---

### Using DI
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->

Within Angular’s DI system, instead of directly importing and creating a new instance of a class, instead we will: 

- Register the “dependency” with Angular 
- Describe how the dependency will be injected 
- Inject the dependency 

<img src="/img/custom/di.png">


Note:
While it’s interesting to see how an injector is created directly, that isn’t the typical way we’d use 
injections. 
Instead, what we’d normally do is 
- use NgModule to register what we’ll inject – these are called providers and 
- use decorators (generally on a constructor) to specify what we’re injecting
---

### Register providers
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->

```
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { UserService } from '../services/user.service';
@NgModule({
imports: [CommonModule],
 providers: [
    UserService // <-- added right here
 ],
 declarations: []
 })
export class UserDemoModule { }
```
The class by itself is actually shorthand notation for the following, equivalent configuration:
```
providers: [{ provide: UserService, useClass: UserService }]
```
Usage:
```
// Angular will inject the singleton instance of `UserService` here. 
// We set it as a property with `private`.
constructor(private userService: UserService) {
}
```
---
### Providers
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->

Configuring providers:
Inject a (singleton) instance of a class, inject a value, call any function and inject the return value of that function
    
```
//Inject value
export class Test {constructor(@Injector('API_URL') apiUrl: string) {}}
```
```
 providers: [
    {
    // `AnalyticsService` is the _token_ we use to inject
    // note, the token is the class, but it's just used as an identifier! 
    provide: AnalyticsService,
    // useFactory is a function - whatever is returned from this function // will be injected
    useFactory() {
        // create an implementation that will log the event
        const loggingImplementation: AnalyticsImplementation = { recordEvent: (metric: Metric): void => {
            console.log('The metric is:', metric);
        }
    };
    // create our new `AnalyticsService` with the implementation
    return new AnalyticsService(loggingImplementation); }
    } ],
```

---
### HTTP
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->
Angular comes with its own HTTP library which we can use to call out to external APIs. 
In Javascript, there are generally three approaches to dealing with async code: 

- Callbacks 
- Promises 
- Observables

```
makeRequest(): void {
    this.http.request('http://jsonplaceholder.typicode.com/posts/1').subscribe((res: Response) => {
        this.data = res.json();
        this.loading = false; 
    });
}
```
```
.subscribe(
    (results: SearchResult[]) => { console.log('success');},
    (err: any) => {console.log(err); //-> on error},
    () => {this.loading.next(false); // -> on completion }); 
```
