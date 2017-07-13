### Angular and NativeScript

<!-- .slide: data-background="img/background-orange-orig.jpg" -->

NativeScript is a cross platform mobile development framework that leverages technologies you already know: JavaScript, 
CSS, and of course, Angular.

- Hybrid <- develop app using web technologies but render in web view
- Native <- use native UI components that Google and Apple made available to developers

---
### Create first mobile app
<!-- .slide: data-background="img/background-orange-orig.jpg" -->

```
tns create ProjectName --ng
//The --ng flag indicate that we want to create Angular with TypeScript project
```

```
tns platform add [platform]
```
```
tns run [platform]
```

```
tns livesync [platform] --emulator --watch
```