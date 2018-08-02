## What is Angular?
* Frontend/ Client Side Javascript framework
* Used to build powerful single page applications
* Part of very powerful MEAN stack
* Kinda like HTML for dynamic web applications

What is Angular Not?
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









