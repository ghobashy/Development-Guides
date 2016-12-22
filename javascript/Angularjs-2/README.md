# Angular js Style Guide

##Table of Contents: 
- [Single Responsibility](#single-responsibility)
_

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