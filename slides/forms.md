### Angular Forms

<!-- .slide: data-background="img/background-green-orig.jpg" -->

- <b>FormControls</b> -> encapsulate the inputs in our forms and give us objects to work with them 
- <b>Validators</b> -> give us the ability to validate inputs, any way we’d like
- <b>Observers</b> -> let us watch our form for changes and respond accordingly

---

### FormControls and FormGroups
<!-- .slide: data-background="img/background-green-orig.jpg" -->

The two fundamental objects in Angular forms are FormControl and FormGroup.

- <b>FormControl</b> -> single input field - it is the smallest unit of an Angular form. 
    FormControls encapsulate the field’s value, and states such as being valid, dirty (changed), or has errors. 
    
- <b>FormGroup</b> -> most forms have more than one field, so we need a way to manage multiple FormControls.
FormGroups solve this issue by providing a wrapper interface around a collection of FormControls.


Note:
We need to add FormModule and ReactiveFormModule as dependency inside app module

FormsModule gives us template driven directives such as:  ngModel and NgForm
ReactiveFormsModule gives us directives like: formControl and ngFormGroup  

---
### Form Example
<!-- .slide: data-background="img/background-green-orig.jpg" -->

```
<div class="ui raised segment">
    <h2 class="ui header">Demo Form: Sku</h2> 
    <form #f="ngForm" (ngSubmit)="onSubmit(f.value)"class="ui form">
        <label for="skuInput">SKU</label>
        <input type="text" id="skuInput" placeholder="SKU" name="sku" ngModel>
        <button type="submit" class="ui button">Submit</button> 
    </form>
</div>
```

---
### Form Builder
<!-- .slide: data-background="img/background-green-orig.jpg" -->
FormBuilder is helper class that helps us build forms. Forms are made up of FormControls and FormGroups 
and the FormBuilder helps us make them (you can think of it as a “factory” object). 


```
import { Component } from '@angular/core'; import {
  FormBuilder,
  FormGroup
} from '@angular/forms';
@Component({
  selector: 'app-demo-form-sku-with-builder',
  templateUrl: './demo-form-sku-with-builder.component.html',
  styles: []
})
export class DemoFormSkuWithBuilderComponent {
    myForm: FormGroup;
  
    constructor(fb: FormBuilder) { 
        this.myForm = fb.group({'sku': ['ABC123']});
    }   
    onSubmit(value: string): void { 
        console.log('you submitted value: ', value);
    } 
}
```

---
### Using Form Builder on template
<!-- .slide: data-background="img/background-green-orig.jpg" -->
When we are using FormsModule that NgForm will be automatically applied to a "form" element.
There is an exception: NgForm won’t be applied to a <form> that has formGroup. 


```
<form [formGroup]="myForm">
    <label for="skuInput">SKU</label>
    <input type="text" id="skuInput" placeholder="SKU" 
    [formControl]="myForm.controls['sku']">
</form>
```
---
### Validators
<!-- .slide: data-background="img/background-green-orig.jpg" -->

```
constructor(fb: FormBuilder) { 
    this.myForm = fb.group({
      'sku':  ['', Validators.required]
    });
    this.sku = this.myForm.controls['sku']; 
}
<!-- HTML Template --> 
<div *ngIf="sku.hasError('required')" class="error message">SKU is required</div>
```

```
export class Validators {
    static required(c: FormControl): StringMap<string, boolean> {
        return isBlank(c.value) || c.value == "" ? {"required": true} : null;
    }
}
//Usage
constructor(fb: FormBuilder) { this.myForm = fb.group({
      'sku':  ['', Validators.compose([Validators.required, skuValidator])]
});
//If we are using more than one validation on one FormControl we need to use Validators.compose
```
---
### Watching for changes
<!-- .slide: data-background="img/background-green-orig.jpg" -->

```
constructor(fb: FormBuilder) { 
    this.myForm = fb.group({'sku':  ['', Validators.required]});
    
    this.sku = this.myForm.controls['sku'];
    
    this.sku.valueChanges.subscribe( (value: string) => {
        console.log('sku changed to:', value);
      }
    );
    
    this.myForm.valueChanges.subscribe( (form: any) => {
        console.log('form changed to:', form);
      }
    );
}
```
