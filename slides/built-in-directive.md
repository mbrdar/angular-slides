### Built in directives
<!-- .slide: data-background="img/background-violet-orig.jpg" -->
NgIf
```
<div *ngIf="false"></div> <!-- never displayed -->
<div *ngIf="a > b"></div> <!-- displayed if a is more than b -->
<div *ngIf="str == 'yes'"></div> <!-- displayed if str is the string "yes" -->
<div *ngIf="myFunc()"></div> <!-- displayed if myFunc returns truthy -->

```
NgSwitch
```
<div class="container" [ngSwitch]="myVar"> 
    <div *ngSwitchCase="'A'">Var is A</div> 
    <div *ngSwitchCase="'B'">Var is B</div>
    <div *ngSwitchCase="'C'">Var is C</div> 
    <div *ngSwitchDefault>Var is something else</div>
</div>
```
---

### Built in directives
<!-- .slide: data-background="img/background-violet-orig.jpg" -->

NgStyle
```
<div [ngStyle]="{color: 'white', 'background-color': 'blue'}">
    Uses fixed white text on blue background
</div>
<!--Another way-->
<div [style.background-color]="'yellow'">
	Uses fixed yellow background
</div>
```
NgClass
```
.bordered {
    border: 1px dashed black; background-color: #eee;
}
<div [ngClass]="{bordered: false}">This is never bordered</div>
<div [ngClass]="{bordered: true}">This is always bordered</div>
```
Be careful when you have class names that contains dashes, like bordered-box.
JavaScript requires that object-literal keys with dashes be quoted like a string.

---
### Built in directives
<!-- .slide: data-background="img/background-violet-orig.jpg" -->

NgFor
```
<!-- The role of this directive is to repeat a given DOM element
(or a collection of DOM elements) and pass an element of the array on each iteration. -->

The syntax is *ngFor="let item of items".
```
NgNonBindable
```
<div class='ngNonBindableDemo'>
    <span class="bordered">{{ content }}</span>
    <span class="pre" ngNonBindable>
        &larr; This is what {{ content }} rendered
    </span>
</div>
```

Note: We use ngNonBindable when we want tell Angular not to compile or bind a particular section of our page.
