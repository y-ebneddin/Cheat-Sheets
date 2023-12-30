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

// TODO: Check this part

If you have any problem with packages you can remove all packages and run this command:
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

## Install Bootstrap & JQuery

Bootstrap & JQuery are two libraries to help make better pages

```
npm install bootstrap[@version]
npm install jquery
```
If you have any problem with packages you can delete node_modules folder from the source folder and run this command to install all packages again:
```
npm install
```
Add these lines in angular.json
- "node_module/bootstrap/dist/css/bootstrap.min.css" subcaste "styles" before "src/styles.css" because priority of style.css is higher than bootstrap.min.css.
- "node_module/jquery/jquery.min.js" subcaste "scripts"
- "node_module/bootstrap/dist/js/bootstrap.min.js" subcaste "scripts" after "jquery.min.js

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
| String Interpolation | `{{variable}}` |
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

**Note**: Angular convert these decorators to [ ] like: *ngIf => [ngIf]
## Parent and Child components
A common pattern in Angular is sharing data between a parent component and one or more child components. Implement this pattern with the `@Input()` and `@Output()` decorators.
Consider the following hierarchy:
```html
<parent-component>
  <child-component></child-component>
</parent-component>
```
### Sending data to a child component
#### Child:
```html
<! --  childComponent.html -->
<p>
  Today's item: {{item}}
</p>
```
```javascript
// childComponent.ts
import { Component, Input } from '@angular/core'; // First, import Input
export class ItemDetailComponent {
  @Input() item = ''; // decorate the property with @Input()
}
```
#### Parent:
```html
<! --  parentComponent.html -->
<app-item-detail [item]="currentItem"></app-item-detail>
```
```javascript
// parentComponent.ts
export class AppComponent {
  currentItem = 'Television';
}
```

[![Sending data to a child component](https://angular.io/generated/images/guide/inputs-outputs/input-diagram-target-source.svg "Sending data to a child component")](https://angular.io/guide/inputs-outputs "Sending data to a child component")

### Sending data to a parent component
#### Child
```html
<! --  childComponent.html -->
<label for="item-input">Add an item:</label>
<input type="text" id="item-input" #newItem>
<button type="button" (click)="addNewItem(newItem.value)">Add to parent's list</button>
```
```javascript
// childComponent.ts
export class ItemOutputComponent {
  @Output() newItemEvent = new EventEmitter<string>();
  addNewItem(value: string) {
    this.newItemEvent.emit(value);
  }
}
```
#### Parent
```html
<! --  parentComponent.html -->
<app-item-output (newItemEvent)="addItem($event)"></app-item-output>
```
```javascript
// childComponent.ts
export class AppComponent {
  items = ['item1', 'item2', 'item3', 'item4'];
  addItem(newItem: string) {
    this.items.push(newItem);
  }
}
```
### Two-way binding
#### Parent
```html
<! --  parentComponent.html -->
<app-sizer [(size)]="fontSizePx"></app-sizer>
<div [style.font-size.px]="fontSizePx">Resizable Text</div>
```
```javascript
// parentComponent.ts
fontSizePx = 16;
```
#### Child
```html
<! --  childComponent.html -->
<div>
  <button type="button" (click)="dec()" title="smaller">-</button>
  <button type="button" (click)="inc()" title="bigger">+</button>
  <span [style.font-size.px]="size">FontSize: {{size}}px</span>
</div>
```
```javascript
// childComponent.ts
export class SizerComponent {
  @Input() size!: number | string;
  @Output() sizeChange = new EventEmitter<number>();

  dec() {
    this.resize(-1);
  }
  inc() {
    this.resize(+1);
  }

  resize(delta: number) {
    this.size = Math.min(40, Math.max(8, +this.size + delta));
    this.sizeChange.emit(this.size);
  }
}
```
The two-way binding syntax is shorthand for a combination of property binding and event binding.
```html
<app-sizer [size]="fontSizePx" (sizeChange)="fontSizePx=$event"></app-sizer>
```
## Reference
### Template variables
Template variables help you use data from one part of a template in another part of the template.
A template variable can refer to the following:
- DOM element within a template
- directive or component
- TemplateRef from an ng-template
- web component

###  Local Reference (Template variables)
```html
<! --  component.html -->
<! --  Use # to decleare a local reference -->
<input #phone placeholder="phone number" />
<!-- lots of other elements -->
<!-- phone refers to the input element; pass its `value` to an event handler -->
<button type="button" (click)="callPhone(phone.value)">Call</button>
```
Just like variables in JavaScript or TypeScript code, template variables are scoped to the template that declares them.
### ViewChild (Decorator)
A decorator to access to DOM elements in a component.
```javascript
@ViewChild(selector, {[static:true] [,read:Token]}) name: typeOfToken
```

```html
<! --  component.html -->
<! --  Use # to decleare a local reference -->
<input #phone placeholder="phone number" />
```
```javascript
<! --  component.ts -->
<! --  Use # to decleare a local reference -->
<input #phone placeholder="phone number" />
```
**Note:** By default (status:false), create view child reference after initialize component and you don't have access to view child in initilizing component event. 
You can use static property to define a view child globally but note that it will make your pages heavy.
**Note:** Use ElementRef API as the last resort when direct access to DOM is needed. Use templating and data-binding provided by Angular instead. Alternatively you can take a look at Renderer2 which provides an API that can be safely used.

```html
<! --  component.html -->
<p #localRef>Test</p>
```
```javascript
<! --  component.ts -->
@ViewChild('localRef') localRef: ElementRef;
constructor(private rendered:Renderer2) {}
public ngAfterViewInit(){
	<! --Dangerous -->
	this.localRef.nativeElement.style.color = 'Red';
	<! -- Instead of the above line: -->
	this.renderer.setStyle(this.localRef.nativeElement, 'color', 'Red');
}
```
#### Access to another component:
```javascript
@ViewChild(ComponentType, {read: ComponentType}) name: ComponentType;
```
#### Access to list of another component:
```javascript
@ViewChildren(ComponentType, {read: ComponentType}) name: QueryList<ComponentType>;
```
### ViewEncapsulation

| Member | Description |
|------------|------------|
| Emulated |Emulates a native Shadow DOM encapsulation behavior by adding a specific attribute to the component's host element and applying the same attribute to all the CSS selectors provided via Component#styles or Component#styleUrls. (This is the default option.)|
| None |Doesn't provide any sort of CSS style encapsulation, meaning that all the styles provided via Component#styles or Component#styleUrls are applicable to any HTML element of the application regardless of their host Component. |
| ShadowDom |Uses the browser's native Shadow DOM API to encapsulate CSS styles, meaning that it creates a ShadowRoot for the component's host element which is then used to encapsulate all the Component's styling. |
```javascript
@Component({
  selector: 'app-root',
  template: `
    <h1>Hello World!</h1>
    <span class="red">Shadow DOM Rocks!</span>
  `,
  styles: [`
    :host {
      display: block;
      border: 1px solid black;
    }
    h1 { color: blue; }
    .red { background-color: red; }
  `],
 encapsulation: ViewEncapsulation.ShadowDom
})
class MyApp {
}
```
## Content of parent in child 
ngContent is a decorator to read content of a parent HTML file in a child component .
```html
<! -- parentComponent.html -->
<app-child>
	<p> Parent content between child tags</p>
</app-child>
```
```html
<! -- childComponent.html -->
<p>Parent: <ng-content></ng-content></p>
```
```html
HTML result:
Parent: Parent content between child tags
```
You have an opportunity to decide on the child component's behaviour from the parent component. Select attribute can accept CSS selectors like class and id.
```html
<! -- childComponent.html -->
<div>
	<ng-content select=".success">Success</ng-content>
</div>
<div>
	<ng-content select=".error">Error</ng-content>
</div>
<div>
	<ng-content select=".warning">Wrning</ng-content>
</div>
```
### Use local (content) variable in child typescript
```html
<! -- parentComponent.html -->
<app-child>
	<p #par> Parent content between child tags</p>
</app-child>
```
```javascript
<! --  childComponent.ts -->
@ContentChild('par') par: ElementRef;
public ngAfterContentInit(){
	<! --  Execute code after initializing content -->
}
public ngAfterContentInit(){
	<! --  Run code after content is changed -->
}
```
