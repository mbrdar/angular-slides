### Styles and Encapsulation
<!-- .slide: data-background="img/background-dark-orig.jpg" -->
Define style inside component: <b>styles</b>, <b>styleUrls</b>

### Encapsulation:
```
encapsulation: ViewEncapsulation.None
```
- <b>Emulated</b> <- default

```
<head>
  <style>.zippy[_ngcontent-1] {
  background: green;
  }</style>
</head>

<div class="zippy" _ngcontent-1>
</div>
```
- <b>Native</b> <- add style tag inside component
- <b>None</b> <- no encapsulation at all

---
### Components vs. Directive
<!-- .slide: data-background="img/background-dark-orig.jpg" -->

- Components come with functionality that makes it easy to add views, but directive can have views also.
- Directive can be used to attach behaviours to element.

```
@HostListener('click') displayMessage(): void { <- attach listener to the element
	 alert(‘message’); 
} 
```
```
@HostBinding('attr.class') cssClass = 'ui message'; <- can be used to set host attributes
```
Note:
Component and directives are closely related, but they are slightly different.
Think of it this way: Components are Directives and Components always have a view. Directives may or may not have a view. 

---
### Content projection
<!-- .slide: data-background="img/background-dark-orig.jpg" -->

Goal is to write markup like this:
```
<div message header="My Message">content1</div> 
```
which will render into more complicated HTML like:
```
<div class="ui message">
    <div class="header">My Message</div> 
    <p>content1</p> 
</div> 
```
```
@Component({
 selector: '[message]',
  template: `<div class="header">{{ header }}</div> 
             <p><ng-content></ng-content></p>`
})
export class MessageComponent implements OnInit {
  @Input() header: string;
  @HostBinding('attr.class') cssClass = 'ui message';
  ngOnInit(): void {
    console.log('header', this.header);
} }
```

---
### Lifecycle hooks
<!-- .slide: data-background="img/background-dark-orig.jpg" -->

Lifecycle hooks are the way Angular allows you to add code that runs before or after each step of the directive or component lifecycle. 

- OnInit  <- properties have been initialized
- OnDestroy  <- instance is destroyed
- DoCheck  <- properties have been changed
- OnChanges  <- if only a particular property changed
- AfterContentInit  <- initialization of the content
- AfterContentChecked <- component check has finished
- AfterViewInit  <- view has been fully initialized
- AfterViewChecked 

Note: 
show example in app
It’s important to note that the OnChanges hook gets overriden by DoCheck so if we implement both, OnChanges will be ignored. 
The other two hooks: AfterViewInit and AfterViewChecked are triggered right after the content ones above
Also, the AfterXXXInit hooks are only called once during the directive lifecycle, while the AfterXXXChecked hooks are called after every change detection cycle. 

---
### Change detection
<!-- .slide: data-background="img/background-dark-orig.jpg" -->

- when a DOM Event occurs (like click, change, etc.) 
- when an HTTP request is resolved 
- when a Timer is trigger (setTimeout or setInterval) 

Change detector is created for each component in the tree.

<img src="/img/custom/change-detection.png" width="400" height="200">

- Customizing change detection

Note:
- Angular scans for changes from top to bottom.
One of the big problems any modern JavaScript framework needs to solve is how to figure out when changes have happened and re-render components accordingly. 
When one of the the components change, no matter where it is in the tree, a change detection pass is triggered for the whole tree.

---
### Zones
<!-- .slide: data-background="img/background-dark-orig.jpg" -->

- sometimes Zones won’t be able to automatically identify changes
- then OnPush strategy can be very useful

Examples of things that is out of the Zones control: third party library, immutable data , Observables 

```
constructor(private changeDetector: ChangeDetectorRef) {}
ngOnInit() {
    this.items.subscribe((v) => {
        console.log('got value', v);
        this.counter++;
        if (this.counter % 5 === 0) {
            this.changeDetector.markForCheck();
        }
    },
    null,
    () => {
        this.changeDetector.markForCheck();
    });
}
```
Note: 
Angular use Zones library to automatically detect changes
these are perfect candidates for using OnPush along with a technique to manually hint Angular that something changed. 
That’s the method we use whenever we want to tell Angular that a change has been made, so the change detector should kick in. 

