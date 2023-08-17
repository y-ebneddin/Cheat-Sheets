# Angular

[TOC]

## What is angular?
Angular is a development platform built on TypeScript, encompassing the following key elements:
- **Component-Based Framework:** Angular offers a framework for constructing scalable web applications through components. A component consists of a TypeScript class with a decorator, an HTML template, and styles. Components provide encapsulation and a clear application structure.
- **Templates:** Each component has an HTML template that defines its view. Angular's templates incorporate dynamic values from the component's data, enabling automatic updates to the DOM when the component's state changes.
- **Directives:** You can add features to your templates by using directives. The most popular directives in Angular are *ngIf and *ngFor.
- **Modules:** Angular NgModules organize related components into functional units. Each application has a root module, conventionally named AppModule.
- **Services:** Services handle logic and data that isn't view-specific.
- **Routing:** Angular Router facilitates navigation between different views and states within an application.
- **Dependency Injection:** Dependency injection allows you to declare dependencies of TypeScript classes without managing their instantiation. Angular handles the instantiation, promoting testability and flexibility in your code.
- **Integrated Libraries:** Angular offers various first-party libraries, such as Angular Router for navigation, Angular Forms for form handling, Angular HttpClient for client-server communication, Angular Animations for animations, Angular PWA for Progressive Web Applications, and Angular Schematics for scaffolding and updates. These libraries enhance the functionality of your applications.
- **Angular CLI:** Angular provides a suite of developer tools to facilitate coding, testing, building, and updating your applications. These tools contribute to an efficient development workflow.

[![Angular Architecture](https://angular.io/generated/images/guide/architecture/overview2.png "Angular Architecture")](https://angular.io/guide/architecture "Angular Architecture")

## Requirements

+ Languages <sub>(Basic Knowledge)</sub>:
	+ HTML
	+ CSS
	+ JavaScript
	+ Typescript
+ Packages:
	+ [Node.js](https://nodejs.org/en/download/current "Node.js")
	+ [Angular CLI](https://angular.io/cli "Angular CLI")
+ Tools <sub>(Editor)</sub>:
	+ [Visual Studio Code](https://code.visualstudio.com/download "Visual Studio Code")

## Installation

Install angular/cli on administrator command prompt
```
> npm install -g @angular/cli
```
Create first project:
```
> ng new `App Name`
```
Run first project:
```
`App Folder`> ng serve
```
Install requirement packages:
```
`App Folder`> npm install
```
## Angular project structure

+ app folder: Your codes
+ Index.html: Main output of the project
+ main.ts: Project starter file
+ style.css : Custom main style sheet
+ package.json: Project dependencies
	+ dependencies: Running requirements
	+ devDependencies: Developing req.
+ angular.json: Project settings
	+ projects/`app name`/ architect/build/assets
	+ projects/`app name`/ architect/build/styles
	+ projects/`app name`/ architect/build/scripts

## Components

A component controls a patch of the screen called a view. It consists of a TypeScript class, an HTML template, and a CSS style sheet. The TypeScript class defines the interaction of the HTML template and the rendered DOM structure, while the style sheet describes its appearance.
Each component is identified by the @Components decorator.
Some attributes of @Components are:
- selector: name of the component
- template: Content of HTML
- templateUrl: Url of UI HTML file
- styleUrls: list of this file style sheets

### Make a component

Make a component with angular/cli:
```
`App Folder`> ng generate component `Component Name`
```
Make a component manually:
- Create `Component name.ts` in the app folder (It is better to create under your component folder)
- Define a component class 
```javascript
@Component({
	  selector: "app-user",
	  templateUrl: "./user.component.html",
	  styleUrls: ["./user.component.scss"]
})
export class UserComponent{
}
```
- Add the component to **AppModule**
```javascript
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { UserComponent } from './user.component';
@NgModule({
	  declarations: [AppComponent, UserComponent],
	  imports: [BrowserModule],
	  providers: [],
	  bootstrap: [AppComponent]})
export class AppModule {}
```

### Using component

- Add a selector of components in an HTML file. 
For example, you can add in the app.Component.html:
```html
<app-user></app-user>
```
- Use in another component as a variable or by dependency injection.

## Selectors

The selector is a property inside the angular component which identifies the directive in a template and triggers the instantiation of the directive. The selector must be unique so that it does not override already existing elements or components available by a number of third-party packages.

There are 3 types of selectors:

| Type | Selector | Example |
|------------|------------|------------|
| Element | `app-user` | `<app-user></app-user>` |
| Class | `.app-user `| `<div class="app-user"></div>` |
| Property | `[app-user]` |`<div app-user></div>`|

## Data binding

Data binding automatically keeps your page up-to-date based on your application's state. You use data binding to specify things such as the source of an image, the state of a button, or data for a particular user.

### HTML File &larr; TS File

| Type | Fromat |
|------------|------------|
| String Interpolation | `app-user` |
| Property Binding | `[Property Name]="Variable"` |

### HTML File &rarr; TS File

| Type | Fromat |
|------------|------------|
| Event Binding | `(Event Name)="function($event)"` |

Example:

```javascript
// component.ts
export class UserComponent{
	name string;
	isEnable : Boolean;
	public OnInputChanged(e: event){
		this.name = (<HTMLInputElement>e.target).value;
	};
}
```
```html
<! -- component.html -->
<p>{{name}}<p>
<button [disabled]="isEnable"><button>
<input type="text" (input)="onInputChanged($event)"><button>
```

### HTML File &harr; TS File
| Type | Fromat |
|------------|------------|
| Two-Way binding | `[(target)]="expression"` |

```javascript
// Follow the previous example:
// component.ts
import { FormsModule } from '@angular/forms;
...
```
```html
<! -- component.html -->
<input type="text" [(ngModule)]="name"><button>
```

## Install Bootstrap & JQuery

```
npm install bootstrap[@version]
npm install jquery
```
If you have any problem with packages you can delete node_modules folder from source folder and run this command to installs all packages again:
npm install
Add this lines in angular.json
- "node_module/bootstrap/dist/css/bootstrap.min.css" subcaste "styles" before "src/styles.css" because priority of style.css is higher than bootstrap.min.css.
- "node_module/jquery/jquery.min.js" subcaste "scripts"
- "node_module/bootstrap/dist/js/bootstrap.min.js" subcaste "scripts" after "jquery.min.js

## Attribute Binding

Attribute binding in Angular helps you set values for attributes directly.

Example:

```sass
// component.css
.small_font_size { font-size:2rem; }
.big_font_size { font-size:8rem; }
```
```html
<! -- component.html -->
<! -- Pay attention to attributes of P tags in the following examples -->
<P [class]="customClassStyle"></p>
<P [style]="conditionVariable ? ‘font-size:2rem’ : ‘font-size:8rem’"></p>
<P [style.font-size]="conditionVariable? ‘2rem’ : ‘8rem’"></p>
<P [style.font-size.rem]="conditionVariable? 2 : 8"></p>
```
```javascript
// component.ts
export class UserComponent{
	customClassStyle = {};
	conditionVariable : boolean;
	ngOnInit(): void {
		this.customStyle = {
			'font-size': this.conditionVariable ? 'small_font_size' : 'big_font_size';
		}
	}
}
```

## Directives

Change the appearance or behavior of DOM elements and Angular components with attribute directives.

|  |   |   |
|------------|------------|------------|
|Creator:| Predefined | Custom |
|Usage:| Attribute | Structural |

### Predefined attribute directives
Change the attribute of elements to as same as the attribute binding
- **ngStyle**
- **ngClass**

### Angular structural directives

- \***ngIf:** is used to conditionally render elements in the DOM based on a provided expression. It is commonly used to display or hide elements based on certain conditions.

```html
<p *ngIf="condition expression"></p>
```

If else structure:

```html
<! -- condition is true show tag <P> else show content of <ng-template> -->
<p *ngIf="condition expression; else elseCondition"></p>
<ng-template #elseCondition></ng-template>
<! -- #elsecondition is a local reference that You will learn later. -->
```

- \***ngFor:** is used for rendering a template element multiple times based on an iterable.

```html
<tr *ngFor="let user of users;">
	<td>{{user.name}}</td>
</tr>
<! --  You can use an index of elements. The "index" is a predefined word. -->
<tr *ngFor="let user of users; let i=index">
	<td>{{ i + "-" + user.name}}</td>
</tr>
```

**Trick:** Avoid rendering the entire list if a limited number of the list has changed.

```html
<! --  component.html -->
<tr *ngFor="let user of users; let i=index; trackby:trackByFunc">
	<td>{{ i + "-" + user.name}}</td>
</tr>
```
```javascript
// component.ts
Public trackByFunc(index:number, el:any)
{
	// Select a unique attribute of elements
	return el.id;
}
```

- \***ngSwitch:** is used to conditionally render content based on a specific expression.

```html
<div [ngSwitch]="num">
	<div *ngSwitchCase="'1'">One</div>
	<div *ngSwitchCase="'2'">Two</div>
	<div *ngSwitchCase="'3'">Three</div>
	<div *ngSwitchCase="'4'">Four</div>
	<div *ngSwitchCase="'5'">Five</div>
	<div *ngSwitchDefault>This is Default</div>
</div>
```










