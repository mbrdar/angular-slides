
### Angular CLI

<!-- .slide: data-background="img/background-orange-orig.jpg" -->

1. Based on Webpack
2. Tool which helps process and bundle our various TypeScript, JavaScript, CSS, HTML, and image files
3. Not a requirement for using Angular
---

### Generating and serving an Angular project
<!-- .slide: data-background="img/background-orange-orig.jpg" -->

```
ng new PROJECT-NAME
cd PROJECT-NAME
ng serve
```
Navigate to http://localhost:4200/. The app will automatically reload if you change any of the source files.

---

### Generating Components, Directives, Pipes and Services
<!-- .slide: data-background="img/background-orange-orig.jpg" -->
```
ng g component my-new-component -> #Component
ng g directive my-new-directive -> #Directive
ng g pipe my-new-pipe -> #Pipe
ng g service my-new-service -> #Service
ng g class my-new-class -> #Class
ng g guard my-new-guard -> #Guard
ng g interface my-new-interface -> #Interface
ng g enum my-new-enum -> #Enum
ng g module my-module -> #Module
```

https://github.com/angular/angular-cli