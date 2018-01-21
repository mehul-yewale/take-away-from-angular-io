## We will have a short look of angular.io

### Why AngularJS-2/4?
- **PLATFORM INDEPENDENT** -- For web, mobile web, native mobile and native desktop app. Support SPA (Single Page Application), offline apps, animations.

- **SPEED & PERFORMANCE** -- Web Workers and server-side rendering, control over scalability, building data models on RxJS, Immutable.js or another push-model.

- **WIDELY DOCUMENTED AND POPULAR** -- Build quickly with simple and declarative template approach. Get intelligents code completion, instant errors, and other feedback in almost every editor and IDE. Lots of information on cloud.  
**Angular CLI**  -- Command line tools: start building fast, add components/files, perform testing, and deployment activities,
   
- **TESTING TOOLING** --  Support karma and jasmine unit testing.  
   [Protractor Automation Tool](https://www.thoughtworks.com/insights/blog/testing-angularjs-apps-protractor) --
   end to end test framework, running in a real browser, interacting with it as a user would.
   It is build on NodeJS, Selenium webDriver, Jasmine, Cucumber and Mocha. (Automation testing can be possible like seleniium)
   Protractor is a NodeJS program that is written in JavaScript, so it can easily identify web elements in an Angular JS application and much more inbuild function which is not availablle in selenium.


### So What is AngularJS?
- Angular is a framework for building client applications in HTML and either JavaScript or a language like **TypeScript** that compiles to JavaScript.
- The framework consists of several libraries, some of them are core and some optional.
- We can write Angular applications by composing HTML templates with Angularized markup, writing component classes to manage those templates, adding application logic in services, and boxing components and services in modules.

### Before starting AngularJS 2/4 (Pre - Requisite)
- HTML & CSS
- Familar with javascirpt -- plain javascipt with object based.
- TypeScript -- is typebase javascript, code can be written as similar to java (with classes, interface). But behind the scene it compiles & create javascript code iteself. (Browser knows javascript)

### System configuration
Install Node.js® and NPM if they are not already on your machine.  
1. **NODE** --  it is JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model (it makes javascript as serverside language & bring javascript language as out of from browser to communicate with os)  
**node -version --> 6.9.x & above (keep it as latest)**
2. **NPM**  -- node package manager  
**npm -version --> 3.x.x and above (keep it as latest)**
3. Some of the global packages installation if it is missing form npm or might me needs to it in updated version.

### Modules -->  @NgModule (@ - refers as a typescript decorator)
Angular apps are modular and Angular has its own modularity system called NgModules.  
Every Angular app has at least one NgModule class, the root module, conventionally named AppModule.  
And this AppModule can be divided into feature modules to maintain performance (lazy loading).  
	
```typescript
	import { NgModule }      from '@angular/core';
	import { BrowserModule } from '@angular/platform-browser';
	@NgModule({
	  imports:      [ BrowserModule ],
	  providers:    [ Logger ],
	  declarations: [ AppComponent ],
	  exports:      [ AppComponent ],
	  bootstrap:    [ AppComponent ]
	})
	export class AppModule { }
```
	
- **NgModule** -- NgModules help organize an application into cohesive blocks of functionality. It identifies the module's own components, directives, and pipes, making some of them public so external components can use them.
- Inbuild modules -- FormsModule, HttpModule, and RouterModule
- main.ts file for launching the app : platformBrowserDynamic().bootstrapModule(AppModule);

### Component : 
**A component controls a patch of screen called a view.**
- We define a component's application logic—what it does to support the view—inside a class. The class interacts with the view through an API of properties and methods.  
- @Component is a typescript decorator function which is created by angular that specifies the Angular metadata for the component. Metadata tells Angular how to process a class. (similar to java annotations).  
- Model-View-Controller (MVC) or Model-View-ViewModel (MVVM). In Angular, the component plays the part of the Controller/ViewModel, and the template represents the view.  
```javascript
	import { Component } from '@angular/core';
	@Component({
	  selector: 'app-heroes',		// the components CSS element selector
	  templateUrl: './heroes.component.html', // the location of the component's template file/ component view.
	  styleUrls: ['./heroes.component.css'] // the location of the component's private CSS styles.
	})
	export class HeroesComponent {	}
	
	import { Component } from '@angular/core';
	@Component({
	  selector: 'app-heroes',	// the components CSS element selector
	  template: '<h1>{{title}}</h1>', // that will be templates to render with component
	  style: `body { color: black; }`  // this css will render with component
	})
	export class HeroesComponent { 
		private title: string = "Welcome"; //variable declaration that will be accessed in html template or template file
		constructor() { }  
	}
```

### Data binding 
**Model to View or View to Model data bindings**  
- Data binding plays an important role in communication between a template and its component.

	Lets assume **View is left-side** and **Model is right side**. Below arrow indicates data-binding direction.  
	1. Interpolation (model to view) -- `{``{``obj.id } }`     **<---**
	2. Property binding  (model to view) -- `[value]`    **<---**
	3. Event Binding (view to model) -- `(click)`     **--->**
	4. Two way data binding (view to model and model to view) -- `[(ng-model)]="value"` **<---  --->**  
	- `<input [(ngModel)]="hero.name"> // but only with form elements`.
- Angular processes all data bindings once per JavaScript event cycle, from the root of the application component tree through all child components. (like dirty checking with angular-1)  
- Data binding is also important for communication between parent and child components. 
- Also we can do binding through propery with prefixes bind, on, bindon.  
	- `[target]="expression"`  is same as `bind-target="expression"`
	- `(target)="expression"` is same as `on-target="expression"`
	- `[(target)]="expression"` is same as `bindon-target="expression"`
- When setting value to property in a non-string datatype, we must use property binding and not an attribute binding. (maintains datatype)
- By default interpolation and property binding works with properties of elements, not attributes. (eg : colspan is attribute)
- Attribute binding : `[attr.colspan]="2"`
	  
### Component Interaction
**Interaction/Communication between parent and child components.**
1. Pass data from parent to child with input property binding --  `@Input('master') masterName: string;`  -- `<my-div [master]="master">`.
2. Intercept input property changes with ngOnChanges() method  -- ngOnChanges will execute if any input property got changed in parent components  -- ngOnChanges(changes: SimpleChange).
3. Parent listens for child event -- `(onVoted)="onVoted($event)"` -- `@Output() onVoted = new EventEmitter<boolean>();`   --  `this.onVoted.emit(true);  // this will call parent component 'onVoted' method`
4. Parent interacts with child via local variable  --  But limited to access only in template itself.  
 You can do both by creating a template reference variable for the child element and then reference that variable within the parent template.  
 **Template reference variable** -- `#fax` is same as `ref-fax`.  the scope of this variable wiil be for entire template  
`<button (click)="timer.stop()">Stop</button>`  // calling child components method  
`<app-countdown-timer #timer></app-countdown-timer> `  //child components 

5. Parent calls an @ViewChild() in component (to solve above problem)  --  
`@ViewChild(CountdownTimerComponent) private timerComponent: CountdownTimerComponent;`   -- child component needs to inject in parent component.  
`start() { this.timerComponent.start();}`  //calling child components method 

6. Parent and children communicate via a angulaar service  --  
- A parent component and its children share a service whose interface enables bi-directional communication within the family. (Recommended one)
- Create service file & inject in both components
- Either observable by RxJS or putting simple getters & setters of into service class

### Directives
**Directives allow you to attach behavior to elements in the DOM**
- Angular templates are dynamic. When Angular renders them, it transforms the DOM according to the instructions given by directives.
- A directive is a class with a @Directive decorator.
- A component is also a directive-with-a-template; a @Component decorator is actually a @Directive decorator extended with template-oriented features.
- There are three kinds of directives in Angular:
   
	1. Components —- only this directives have template.
	2. Structural directives —- change the DOM layout by adding. removing and manupulation DOM elements.(eg: *ngFor,*ngIf)
	- Recognize by An asterisk (*) precedes the directive
	- You can apply many attribute directives to one host element. You can only apply one structural directive to a host element.
	3. Attribute directives -— change the appearance or behavior of an element, component, or another directive.( eg: ngStyle, ngClass)
	
```
import { Directive } from '@angular/core';
@Directive({
	selector: '[appHighlight]'   // It's the brackets ([]) that make it an attribute selector
})
export class HighlightDirective {
	constructor() { }
}

@Directive({ 
	selector?: string
	inputs?: string[]
	outputs?: string[]
	host?: {[key: string]: string}
	providers?: Provider[]
	exportAs?: string
	queries?: {[key: string]: any}
})

-- instead of host property above-- 
@HostListener('mouseenter') onMouseEnter() {
	this.highlight(this.highlightColor || 'red');
}
```

### Services 
- Reusable code across all components. Components are big consumers of services. Component classes should be lean. 
- Singleton object shared across the module or components depending upon it's injection.
- Registering at a component level means you get a new instance of the service with each new instance of that component.
 
LoggerService -:  

```
export class LoggerService {
	log(msg: any)   { console.log(msg); }
	error(msg: any) { console.error(msg); }
	warn(msg: any)  { console.warn(msg); }
}
```
### Dependency injection 
 - Dependency injection is a way to supply a new instance of a class with the fully-formed dependencies it requires. Most dependencies are services. Angular uses dependency injection to provide new components with the services they need.
 - Angular can tell which services a component needs by looking at the types of its constructor parameters.  
  `constructor(private logger: LoggerService) { }`
 - When Angular creates a component, it first asks an injector for the services that the component requires.
 - A provider is something that can create or return a service, typically the service class itself. You can register providers in modules or in components.
 - In general, add providers to the root module so that the same instance of a service is available everywhere.
 - Adding providers at a component level means you get a new instance of the service with each new instance of that component.
	
### Change Detection & Angular life cycle hooks 
- Angular executes template expressions, all the data-binided propertis after every change detection cycle. Change detection cycles are triggered by many asynchronous activities such as promise resolutions, http results, timer events, keypresses and mouse events.

### Lifecycle hooks 
**A component has a lifecycle managed by Angular.**
- Angular creates it, renders it, creates and renders its children, checks it when its data-bound properties change, and destroys it before removing it from the DOM.
- A directive has the same set of lifecycle hooks, minus the hooks that are specific to component content and views.  
**LIFECYCLE SEQUENCE :** 
- constructor --  all the dependency injections will be placed here so that before creating component instance, instace propertise get initilized
- ngOnChanges() -- Respond when Angular (re)sets data-bound input properties. The method receives a SimpleChanges object of current and previous property values. Called before ngOnInit() and whenever one or more data-bound input properties change.
- ngOnInit() -- it calls only once after data-bound propertise set (after first ngOnChanges call)
   - To perform complex initializations shortly after construction.
   - To set up the component after Angular sets the input properties.
- ngDoCheck() -- like angular first $scope.digest(); (custom change detection) -- Detect and act upon changes that Angular can't or won't detect on its own. Called during every change detection run, immediately after ngOnChanges() and ngOnInit().
- ngOnDestroy() -- Cleanup just before Angular destroys the directive/component. It helps to unsubscribe observables, detach event handlers, stop interval timers, unregister all callbacks to avoid memory leaks. Called just before Angular destroys the directive/component.  

- There are also component specific hooks (rarely used):  
 -- ngAfterContentInit, ngAfterContentChecked, ngAfterViewInit, ngAfterViewChecked 


### #Follow Me
---
[Github](https://github.com/MehulYewale) | [Twitter](https://twitter.com/mehuly17) | [LinkedIn](https://in.linkedin.com/in/mehul-yewale) | [More Blogs](https://mehul-yewale.github.io/)
