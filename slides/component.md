
### Angular Component

<!-- .slide: data-background="img/background-green-orig.jpg" -->

One of the big ideas behind Angular is the idea of components. 
Fundamental idea behind components is to teach the browser new tags that have custom functionality attached to them.

```
import { Component } from '@angular/core'; 
@Component({ //<- Decorator
  selector: 'greeter',
  template: '<p>{{name}} says welcome!</p>',
})
 export class GreeterComponent { //<- Class
  name: string;
  constructor() {
    this.name='codecentric';
  }
} 
```
```
<greeter></greeter> 

```

Note:
The Application is simply a Component that renders other Components. 
One of the great things about Components is that they’re composable. 
This means that we can build up larger Components from smaller ones. 
Because Components are structured in a parent/child tree, when each Component renders, it recursively renders its children Components. 

Browser only understands a limited set of markup tags built-ins like <select> or <form> or <video> all have functionality defined by our browser creator.
Fundamental idea behind components is to teach the browser new tags that have custom functionality attached to them.
(If you have a background in AngularJS 1.X, you can think of components as the new version of directives. )

Components has two parts:
    -Decorator
    -Class
    

---

### Component Input
<!-- .slide: data-background="img/background-green-orig.jpg" -->

```
import { Component, Input } from '@angular/core'; 
@Component({
  selector: 'my-component',
  template: '<p>My component</p>',
})
 export class MyComponent {
  @Input() name: string;
  @Input() age: number;
} 
```
```
<my-component [name]=“myName" [age]="myAge"></my-component> 

```

---

### Component Output
<!-- .slide: data-background="img/background-green-orig.jpg" -->

```
@Component({
  selector: 'single-component',
  template: '<button> (click)="liked()">Like it?</button>',
})
 export class SingleComponent {
  @Output() putRingOnIt: EventEmitter<string>;
  constructor() {
    this.putRingOnIt = new EventEmitter();
  }
  
  liked(): void {
    this.putRingOnIt.emit('oh oh oh');
  }
} 
```
```
<div>
  <single-component
    (putRingOnIt)="ringWasPlaced($event)"></single-component>
</div>

```

Note:
Constructor — function that is called when we create new instances of this class. 
We can use it to inject services that component uses.

---

### Data Binding
<!-- .slide: data-background="img/background-green-orig.jpg" -->

- One-way data binding <- recommended 
- Two-way data binding

<img src="/img/custom/angular-data-binding.jpg">


---

### Property and Event Binding 
<!-- .slide: data-background="img/background-green-orig.jpg" -->

Property binding:
```
[value]="username"
```
Binds the expression username to the input element’s value property.

Event binding:
```
//(click)=”expression”
<button (click)="triggerChange(value)">Click!</button>
```
Is a declarative way of binding an expression to the input element click event.

---

### Two way data binding
<!-- .slide: data-background="img/background-green-orig.jpg" -->

Using two-way binding with ngModel directive:
```
<input [(ngModel)]="username">
<p>Hello {{username}}!</p>
```

Here’s what our example looks like using ngModel, but without using the shorthand syntax:
```
<input [ngModel]="username" (ngModelChange)="username = $event">
<p>Hello {{username}}!</p>

```

Without the ngModel directive, we can easily implement two-way data bindings just like this:
```
<input [value]="username" (input)="username = $event.target.value">
<p>Hello {{username}}!</p>
```
