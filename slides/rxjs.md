### RxJS
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->

<img src="/img/custom/rxjs.png">

Note:
Observable - is a wrapper around some data source. Data source -> stream of values
Now we have stream of data and we want to do something every time when new value occurs —> this is a job of Observer
Observer is there to execute code whenever we receive new value or error code
we use subscription to connect observer to observable
Observer implements up to 3 methods -> success, error and done
Next method will be call by observable whenever new value is emitted.
Same for other 2 methods.
Some observables will never finish. For example if you wrap click button.
Power of observables is that data goes from top to bottom and we can use various operators.
---
### RxJS Operators
<!-- .slide: data-background="img/background-lightgreen-orig.jpg" -->

<img src="/img/custom/operator.png">
