# Angular  JS Intro
### What is Angular?
* Frontend/ Client Side Javascript framework
* Used to build powerful single page applications
* Part of very powerful MEAN stack
* Kinda like HTML for dynamic web applications

### What is Angular Not?
* Not a server side framework
* Not a js library like (jquery, React etc)
* Not a design pattern like (MVC)
* Not a broswer extension

## History:

* Created as a competitor to ember.js
* Angular 1 based on controller and scopes
* Angular 2 (complete rewrite)-> added components (more to compete with react)
* Angular 3 (issues with router package going out of sync)
* Angular 4 => Backward compatible with Angular 2 and most of changes are under the hood, cleaned it up 


### Why use Angular over Javascript?

1) Rapid development 
Routing
Event Handling
Validation 
very quickly with small fraction of code over js or jquery

2) Code organization and productivity
3) Dynamic content with in html content using directives
4) Completely cross platform 
5) Unit Testing Ready

### Core features and terms:
```
Components
Services
Data Binding
Templating
Directives
Observables
Forms Module
Directivess
Pipes
Events
Animation
TypeScript
Routing
Testing
```

What is TypeScript?

* Superset of Javascript and adds some features
* Optional static typing (string, number, boolean)
* class based object oriented programming (like in java, php)


## Components
1. import component from angular core
import{Component} from '@angular/core'

2. decorate (part of typescript to attach metadata) 
Selector => custom html tage we are going to use in the app
template => can be html along with dynamic properties of variables and also use directives like `if`
@Component({
	selector: 'my-app', 
	template:`<h1>Hello {{name}}</h1>` }
)
>Note: you can also you separate html file for your template
3. we can export the component with a name
export class AppComponent {
	name = 'Angular';
}

4. now to use it like below in html
```

<body>
 <my-app> Loading App Component content here .. </my-app>
</body>

```

So here we get to use our own custom tags and 

## Services

* When you want to share data across multiple components. 
Then we can inject the service into components and use the data in each one.

1. We import Injectable package from angular core

2. we annotate using decorator @Injectable()
and then export the class

```
@Injectable()
export class UserService {
	getUsers():User[] {
		return USERS;
	}
}

```


### Installation
``` 
npm install -g @angular/cli

```

### Create a new angular app
``` 
ng new a4app 

```

### Start the server
```
ng serve

```
Starts up the server on 4200.

[Localhost url](http://localhost:4200)

> Note: Look at package.json, angular.json 

### Look inside the src

Then you can look at src/app folder
```
app.module.ts  => all the components used in applicatoin needs to be brought in here.

app.component.ts => the app component class (typescript)

app.component.html => app components template

app.component.css => app components css

app.component.spec.ts => for tests

```

### To generate new component called user
``` 
ng g component components/user

```
> Note: To open terminal in vscode type `` ctrl + ` ``
> Note: It imports this and also adds to declarations in app.module.ts automatically
### look inside component.ts
  * We have Constructor 
  * We also have `ngOnInit()` => lifecycle hook 

  ```

	export class UserComponent implements OnInit {

	  // Defines a model with static typing on the field types
	  // Defines a model with static typing on the field types
	  name:string;  // name is type string
	  age:number;  // age is type number
	  email:string; //email is a string
	  address:Address; // address is of type Address
	  hobbies:string[]; // hobbies is a string array
	  hello:any; // hello can accept any type of data
  
	  constructor() { 
	    this.name = "heyllo"; //`this` refers to itself. 
	    this.address = {
	      street: "street1",
	      city: "san francisco",
	      state: "CA"
	  }
    
    //so this.name means name inside of itself
  }

	  ngOnInit() { //Life cycle method
	  }

}


  ```

### Creating custom types
* you can create a new custom type using `interface`. Eg: think of an address of a user which can contain street, apt and zipcode.

```
// A custom complex type Address
interface Address{
  street:string,
  city:string,
  state:string,
}

```

###
user template can be like below:
```
<h1>{{name}}</h1>
<ul>
  <li>Age: {{age}}</li>
  <li> Email: {{email}}</li>
  <li> {{address.street}} {{address.city}} {{address.state}}</li>
</ul>

```

### Handling loops with directive (ng-loop)

```
<h1>hobbies</h1>
<ul>
  <li *ngFor ="let hobby of hobbies">{{hobby}}</li>
</ul>

```
> Note: creates multiple `li` items and uses `hobby` as looping variable over array `hobbies` 






