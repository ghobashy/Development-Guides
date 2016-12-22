# Angular 2 js Style Guide

##Table of Contents: 
- [Single Responsibility](#single-responsibility)
- [Naming](#naming)
- [Coding Conventions](#coding-conventions)
- [Components](#components)


##Single Responsibility

- Do define one thing (e.g. service or component) per file.

- Consider limiting files to 400 lines of code.

*Why?*: One component per file makes it far easier to read, maintain, and avoid collisions with teams in source control.

*Why?*: One component per file avoids hidden bugs that often arise when combining components in a file where they may share variables, create unwanted closures, or unwanted coupling with dependencies.

*Why?*: A single component can be the default export for its file which facilitates lazy loading with the Router.

The key is to make the code more reusable, easier to read, and less mistake prone.

The following negative example defines the AppComponent, bootstraps the app, defines the Hero model object, and loads heroes from the server ... all in the same file. Don't do this.

```typescript
	/* avoid */
	import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
	import { BrowserModule } from '@angular/platform-browser';
	import { NgModule, Component, OnInit } from '@angular/core';
	class Hero {
	  id: number;
	  name: string;
	}
	@Component({
	  selector: 'my-app',
	  template: `
	      <h1>{{title}}</h1>
	      <pre>{{heroes | json}}</pre>
	    `,
	  styleUrls: ['app/app.component.css']
	})
	class AppComponent implements OnInit {
	  title = 'Tour of Heroes';
	  heroes: Hero[] = [];
	  ngOnInit() {
	    getHeroes().then(heroes => this.heroes = heroes);
	  }
	}
	@NgModule({
	  imports: [ BrowserModule ],
	  declarations: [ AppComponent ],
	  exports: [ AppComponent ],
	  bootstrap: [ AppComponent ]
	})
	export class AppModule { }
	platformBrowserDynamic().bootstrapModule(AppModule);
	const HEROES: Hero[] = [
	  {id: 1, name: 'Bombasto'},
	  {id: 2, name: 'Tornado'},
	  {id: 3, name: 'Magneta'},
	];
	function getHeroes(): Promise<Hero[]> {
	  return Promise.resolve(HEROES); // TODO: get hero data from the server;
	}
```

Better to redistribute the component and supporting activities into their own dedicated files.

#### main.ts

```typescript
	import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
	import { AppModule }      from './app/app.module';
	platformBrowserDynamic().bootstrapModule(AppModule);
```
#### app/app.module.ts

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { RouterModule } from '@angular/router';
import { AppComponent } from './app.component';
import { HeroesComponent } from './heroes/heroes.component';
@NgModule({
  imports: [
    BrowserModule,
  ],
  declarations: [
    AppComponent,
    HeroesComponent
  ],
  exports: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }


```
#### app/app.component.ts

```typescript
import { Component } from '@angular/core';
import { HeroService } from './heroes';
@Component({
  moduleId: module.id,
  selector: 'toh-app',
  template: `
      <toh-heroes></toh-heroes>
    `,
  styleUrls: ['app.component.css'],
  providers: [ HeroService ]
})
export class AppComponent { }
```

#### app/heroes/heroes.component.ts

```typescript
import { Component, OnInit } from '@angular/core';
import { Hero, HeroService } from './shared';
@Component({
  selector: 'toh-heroes',
  template: `
      <pre>{{heroes | json}}</pre>
    `
})
export class HeroesComponent implements OnInit {
  heroes: Hero[] = [];
  constructor(private heroService: HeroService) {}
  ngOnInit() {
    this.heroService.getHeroes()
      .then(heroes => this.heroes = heroes);
  }
}

```

#### app/heroes/shared/hero.service.ts

```typescript
import { Injectable } from '@angular/core';
import { HEROES } from './mock-heroes';
@Injectable()
export class HeroService {
  getHeroes() {
    return Promise.resolve(HEROES);
  }
}

```

#### app/heroes/shared/hero.model.ts

```typescript
export class Hero {
  id: number;
  name: string;
}


```

#### app/heroes/shared/mock-heroes.ts

```typescript
import { Hero } from './hero.model';
export const HEROES: Hero[] = [
  {id: 1, name: 'Bombasto'},
  {id: 2, name: 'Tornado'},
  {id: 3, name: 'Magneta'},
];

```

As the app grows, this rule becomes even more important.


### Small Functions


Do define small functions

Consider limiting to no more than 75 lines.

*Why?* Small functions are easier to test, especially when they do one thing and serve one purpose.

*Why?* Small functions promote reuse.

*Why?* Small functions are easier to read.

*Why?* Small functions are easier to maintain.

*Why?* Small functions help avoid hidden bugs that come with large functions that share variables with external scope, create unwanted closures, or unwanted coupling with dependencies.

##Naming

To be done

##Coding Conventions

Have consistent set of coding, naming, and whitespace conventions.

###Classes

Do use upper camel case when naming classes.

*Why?* Follows conventional thinking for class names.

*Why?* Classes can be instantiated and construct an instance. By convention, upper camel case indicates a constructable asset.

####app/shared/exception.service.ts
```typescript
/* avoid */
export class exceptionService {
  constructor() { }
}
```

####app/shared/exception.service.ts
```typescript
export class ExceptionService {
  constructor() { }
}
```
###Constants

Do declare variables with const if their values should not change during the application lifetime.

*Why?* Conveys to readers that the value is invariant.

*Why?* TypeScript helps enforce that intent by requiring immediate initialization and by preventing subsequent re-assignment.

Consider spelling const variables in lower camel case.

*Why?* lower camel case variable names (heroRoutes) are easier to read and understand than the traditional UPPER_SNAKE_CASE names (HERO_ROUTES).

*Why?* The tradition of naming constants in UPPER_SNAKE_CASE reflects an era before the modern IDEs that quickly reveal the const declaration. TypeScript itself prevents accidental reassignment.

Do tolerate existing const variables that are spelled in UPPER_SNAKE_CASE.

*Why?* The tradition of UPPER_SNAKE_CASE remains popular and pervasive, especially in third party modules. It is rarely worth the effort to change them or the risk of breaking existing code and documentation.

####app/shared/data.service.ts
```typescript
export const mockHeroes   = ['Sam', 'Jill']; // prefer
export const heroesUrl    = 'api/heroes';    // prefer
export const VILLAINS_URL = 'api/villains';  // tolerate
```
###Interfaces
Do name an interface using upper camel case.

Consider naming an interface without an I prefix.

Consider using a class instead of an interface.

*Why?* TypeScript guidelines discourage the "I" prefix.

*Why?* A class alone is less code than a class-plus-interface.

*Why?* A class can act as an interface (use implements instead of extends).

*Why?* An interface-class can be a provider lookup token in Angular dependency injection.


####app/shared/hero-collector.service.ts
```typescript
/* avoid */
import { Injectable } from '@angular/core';
import { IHero } from './hero.model.avoid';
@Injectable()
export class HeroCollectorService {
  hero: IHero;
  constructor() { }
}
```

####app/shared/hero-collector.service.ts
```typescript
import { Injectable } from '@angular/core';
import { Hero } from './hero.model';
@Injectable()
export class HeroCollectorService {
  hero: Hero;
  constructor() { }
}

```

###Properties and Methods
Do use lower camel case to name properties and methods.

Avoid prefixing private properties and methods with an underscore.

*Why?* Follows conventional thinking for properties and methods.

*Why?* JavaScript lacks a true private property or method.

*Why?* TypeScript tooling makes it easy to identify private vs public properties and methods.

####app/shared/toast.service.ts
```typescript
/* avoid */
import { Injectable } from '@angular/core';
@Injectable()
export class ToastService {
  message: string;
  private _toastCount: number;
  hide() {
    this._toastCount--;
    this._log();
  }
  show() {
    this._toastCount++;
    this._log();
  }
  private _log() {
    console.log(this.message);
  }
}
```
####app/shared/toast.service.ts
```typescript
import { Injectable } from '@angular/core';
@Injectable()
export class ToastService {
  message: string;
  private toastCount: number;
  hide() {
    this.toastCount--;
    this.log();
  }
  show() {
    this.toastCount++;
    this.log();
  }
  private log() {
    console.log(this.message);
  }
}
```

##Components

###Component Selector Naming
Do use dashed-case or kebab-case for naming the element selectors of components.

*Why?* Keeps the element names consistent with the specification for Custom Elements.

####app/heroes/shared/hero-button/hero-button.component.ts
```typescript
/* avoid */
@Component({
  selector: 'tohHeroButton',
  templateUrl: 'hero-button.component.html'
})
export class HeroButtonComponent {}
```
####app/heroes/shared/hero-button/hero-button.component.ts
```typescript
@Component({
  selector: 'toh-hero-button',
  templateUrl: 'hero-button.component.html'
})
export class HeroButtonComponent {}

####app/app.component.html
```typescript
<toh-hero-button></toh-hero-button>
```
###Components as Elements

Do define components as elements via the selector.

*Why?* components have templates containing HTML and optional Angular template syntax. They are most associated with putting content on a page, and thus are more closely aligned with elements.

*Why?* A component represents a visual element on the page. Defining the selector as an HTML element tag is consistent with native HTML elements and WebComponents.

*Why?* It is easier to recognize that a symbol is a component vs a directive by looking at the template's html.

####app/heroes/hero-button/hero-button.component.ts
```typescript
/* avoid */
@Component({
  selector: '[tohHeroButton]',
  templateUrl: 'hero-button.component.html'
})
export class HeroButtonComponent {}

```
####app/app.component.html
```typescript
<!-- avoid -->
<div tohHeroButton></div>

```
####app/heroes/hero-button/hero-button.component.ts
```typescript
@Component({
  selector: 'toh-hero-button',
  templateUrl: 'hero-button.component.html'
})
export class HeroButtonComponent {}

```
####app/app.component.html
```typescript
<toh-hero-button></toh-hero-button>
```

###Extract Template and Styles to Their Own Files

Do extract templates and styles into a separate file, when more than 3 lines.

Do name the template file [component-name].component.html, where [component-name] is the component name.

Do name the style file [component-name].component.css, where [component-name] is the component name.

*Why?* Syntax hints for inline templates in (.js and .ts) code files are not supported by some editors.

*Why?* A component file's logic is easier to read when not mixed with inline template and styles.

####app/heroes/heroes.component.ts
```typescript
/* avoid */
@Component({
  selector: 'toh-heroes',
  template: `
    <div>
      <h2>My Heroes</h2>
      <ul class="heroes">
        <li *ngFor="let hero of heroes">
          <span class="badge">{{hero.id}}</span> {{hero.name}}
        </li>
      </ul>
      <div *ngIf="selectedHero">
        <h2>{{selectedHero.name | uppercase}} is my hero</h2>
      </div>
    </div>
  `,
  styleUrls:  [`
    .heroes {
      margin: 0 0 2em 0; list-style-type: none; padding: 0; width: 15em;
    }
    .heroes li {
      cursor: pointer;
      position: relative;
      left: 0;
      background-color: #EEE;
      margin: .5em;
      padding: .3em 0;
      height: 1.6em;
      border-radius: 4px;
    }
    .heroes .badge {
      display: inline-block;
      font-size: small;
      color: white;
      padding: 0.8em 0.7em 0 0.7em;
      background-color: #607D8B;
      line-height: 1em;
      position: relative;
      left: -1px;
      top: -4px;
      height: 1.8em;
      margin-right: .8em;
      border-radius: 4px 0 0 4px;
    }
  `]
})
export class HeroesComponent implements OnInit {
  heroes: Hero[];
  selectedHero: Hero;
  ngOnInit() {}
}
```

####app/heroes/heroes.component.ts
```typescript
@Component({
  selector: 'toh-heroes',
  templateUrl: 'heroes.component.html',
  styleUrls:  ['heroes.component.css']
})
export class HeroesComponent implements OnInit {
  heroes: Hero[];
  selectedHero: Hero;
  ngOnInit() { }
}
```
####app/heroes/heroes.component.html
```typescript
<div>
  <h2>My Heroes</h2>
  <ul class="heroes">
    <li *ngFor="let hero of heroes">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </li>
  </ul>
  <div *ngIf="selectedHero">
    <h2>{{selectedHero.name | uppercase}} is my hero</h2>
  </div>
</div>

```
####app/heroes/heroes.component.css

```typescript
.heroes {
  margin: 0 0 2em 0; list-style-type: none; padding: 0; width: 15em;
}
.heroes li {
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  height: 1.6em;
  border-radius: 4px;
}
.heroes .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: -4px;
  height: 1.8em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```
###Decorate Input and Output Properties Inline

Do use `@Input` and `@Output` instead of the `inputs` and `outputs` properties of the `@Directive` and `@Component` decorators:

Do place the `@Input()` or `@Output()` on the same line as the property they decorate.

*Why?* It is easier and more readable to identify which properties in a class are inputs or outputs.

*Why?* If you ever need to rename the property or event name associated with `@Input` or `@Output`, you can modify it a single place.

*Why?* The metadata declaration attached to the directive is shorter and thus more readable.

*Why?* Placing the decorator on the same line makes for shorter code and still easily identifies the property as an input or output.

####app/heroes/shared/hero-button/hero-button.component.ts
```typescript
/* avoid */
@Component({
  selector: 'toh-hero-button',
  template: `<button></button>`,
  inputs: [
    'label'
  ],
  outputs: [
    'change'
  ]
})
export class HeroButtonComponent {
  change = new EventEmitter<any>();
  label: string;
}

```
####app/heroes/shared/hero-button/hero-button.component.ts
```typescript
@Component({
  selector: 'toh-hero-button',
  template: `<button>{{label}}</button>`
})
export class HeroButtonComponent {
  @Output() change = new EventEmitter<any>();
  @Input() label: string;
}
```

###Avoid Renaming Inputs and Outputs

Avoid renaming inputs and outputs, when possible.

*Why?* May lead to confusion when the output or the input properties of a given directive are named a given way but exported differently as a public API.

####app/heroes/shared/hero-button/hero-button.component.ts
```typescript
/* avoid */
@Component({
  selector: 'toh-hero-button',
  template: `<button>{{label}}</button>`
})
export class HeroButtonComponent {
  @Output('changeEvent') change = new EventEmitter<any>();
  @Input('labelAttribute') label: string;
}

```
####app/app.component.html
```typescript
<!-- avoid -->
<toh-hero-button labelAttribute="OK" (changeEvent)="doSomething()">
</toh-hero-button>
```
####app/heroes/shared/hero-button/hero-button.component.ts
```typescript
@Component({
  selector: 'toh-hero-button',
  template: `<button>{{label}}</button>`
})
export class HeroButtonComponent {
  @Output() change = new EventEmitter<any>();
  @Input() label: string;
}
```
####app/app.component.html
```typescript
<toh-hero-button label="OK" (change)="doSomething()">
</toh-hero-button>
```

###Member Sequence

Do place properties up top followed by methods.

Do place private members after public members, alphabetized.

*Why?* Placing members in a consistent sequence makes it easy to read and helps instantly identify which members of the component serve which purpose.

####app/shared/toast/toast.component.ts
```typescript
/* avoid */
export class ToastComponent implements OnInit {
  private defaults = {
    title: '',
    message: 'May the Force be with You'
  };
  message: string;
  title: string;
  private toastElement: any;
  ngOnInit() {
    this.toastElement = document.getElementById('toh-toast');
  }
  // private methods
  private hide() {
    this.toastElement.style.opacity = 0;
    window.setTimeout(() => this.toastElement.style.zIndex = 0, 400);
  }
  activate(message = this.defaults.message, title = this.defaults.title) {
    this.title = title;
    this.message = message;
    this.show();
  }
  private show() {
    console.log(this.message);
    this.toastElement.style.opacity = 1;
    this.toastElement.style.zIndex = 9999;
    window.setTimeout(() => this.hide(), 2500);
  }
}
```
####app/shared/toast/toast.component.ts
```typescript
export class ToastComponent implements OnInit {
  // public properties
  message: string;
  title: string;
  // private fields
  private defaults = {
    title: '',
    message: 'May the Force be with You'
  };
  private toastElement: any;
  // public methods
  activate(message = this.defaults.message, title = this.defaults.title) {
    this.title = title;
    this.message = message;
    this.show();
  }
  ngOnInit() {
    this.toastElement = document.getElementById('toh-toast');
  }
  // private methods
  private hide() {
    this.toastElement.style.opacity = 0;
    window.setTimeout(() => this.toastElement.style.zIndex = 0, 400);
  }
  private show() {
    console.log(this.message);
    this.toastElement.style.opacity = 1;
    this.toastElement.style.zIndex = 9999;
    window.setTimeout(() => this.hide(), 2500);
  }
}
```

###Put Logic in Services

Do limit logic in a component to only that required for the view. All other logic should be delegated to services.

Do move reusable logic to services and keep components simple and focused on their intended purpose.

*Why?* Logic may be reused by multiple components when placed within a service and exposed via a function.

*Why?* Logic in a service can more easily be isolated in a unit test, while the calling logic in the component can be easily mocked.

*Why?* Removes dependencies and hides implementation details from the component.

*Why?* Keeps the component slim, trim, and focused.

####app/heroes/hero-list/hero-list.component.ts
```typescript
/* avoid */
import { OnInit } from '@angular/core';
import { Http, Response } from '@angular/http';
import { Observable } from 'rxjs/Observable';
import { Hero } from '../shared/hero.model';
const heroesUrl = 'http://angular.io';
export class HeroListComponent implements OnInit {
  heroes: Hero[];
  constructor(private http: Http) {}
  getHeroes() {
    this.heroes = [];
    this.http.get(heroesUrl)
      .map((response: Response) => <Hero[]>response.json().data)
      .catch(this.catchBadResponse)
      .finally(() => this.hideSpinner())
      .subscribe((heroes: Hero[]) => this.heroes = heroes);
  }
  ngOnInit() {
    this.getHeroes();
  }
  private catchBadResponse(err: any, source: Observable<any>) {
    // log and handle the exception
    return new Observable();
  }
  private hideSpinner() {
    // hide the spinner
  }
}
```
####app/heroes/hero-list/hero-list.component.ts
```typescript
import { Component, OnInit } from '@angular/core';
import { Hero, HeroService } from '../shared';
@Component({
  selector: 'toh-hero-list',
  template: `...`
})
export class HeroListComponent implements OnInit {
  heroes: Hero[];
  constructor(private heroService: HeroService) {}
  getHeroes() {
    this.heroes = [];
    this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
  }
  ngOnInit() {
    this.getHeroes();
  }
}
```

###Don't Prefix Output Properties

Do name events without the prefix on.

Do name event handler methods with the prefix on followed by the event name.

*Why?* This is consistent with built-in events such as button clicks.

*Why?* Angular allows for an alternative syntax on-*. If the event itself was prefixed with on this would result in an on-onEvent binding expression.

####app/heroes/hero.component.ts
```typescript
/* avoid */
@Component({
  selector: 'toh-hero',
  template: `...`
})
export class HeroComponent {
  @Output() onSavedTheDay = new EventEmitter<boolean>();
}
```
####app/app.component.html
```typescript
<!-- avoid -->
<toh-hero (onSavedTheDay)="onSavedTheDay($event)"></toh-hero>
```
####app/heroes/hero.component.ts
```typescript
export class HeroComponent {
  @Output() savedTheDay = new EventEmitter<boolean>();
}
```
####app/app.component.html
```typescript
<toh-hero (savedTheDay)="onSavedTheDay($event)"></toh-hero>
```

###Put Presentation Logic in the Component Class

Do put presentation logic in the component class, and not in the template.

*Why?* Logic will be contained in one place (the component class) instead of being spread in two places.

*Why?* Keeping the component's presentation logic in the class instead of the template improves testability, maintainability, and reusability.

####app/heroes/hero-list/hero-list.component.ts
```typescript
/* avoid */
@Component({
  selector: 'toh-hero-list',
  template: `
    <section>
      Our list of heroes:
      <hero-profile *ngFor="let hero of heroes" [hero]="hero">
      </hero-profile>
      Total powers: {{totalPowers}}<br>
      Average power: {{totalPowers / heroes.length}}
    </section>
  `
})
export class HeroListComponent {
  heroes: Hero[];
  totalPowers: number;
}
```
####app/heroes/hero-list/hero-list.component.ts
```typescript
@Component({
  selector: 'toh-hero-list',
  template: `
    <section>
      Our list of heroes:
      <toh-hero *ngFor="let hero of heroes" [hero]="hero">
      </toh-hero>
      Total powers: {{totalPowers}}<br>
      Average power: {{avgPower}}
    </section>
  `
})
export class HeroListComponent {
  heroes: Hero[];
  totalPowers: number;
  get avgPower() {
    return this.totalPowers / this.heroes.length;
  }
}

```