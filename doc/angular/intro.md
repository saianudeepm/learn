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
0. Generate component like so:
```
ng generate component components/<component_name>

```
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

0. Generate a service using:
```
ng generate service services/<service_name>
```
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

### Handling loops with directive (ngFor)

```
<h1>hobbies</h1>
<ul>
  <li *ngFor ="let hobby of hobbies">{{hobby}}</li>
</ul>

```
> Note: creates multiple `li` items and uses `hobby` as looping variable over array `hobbies` 

#### We can also access the index inside this loop like below
```
<ul>
  <li *ngFor ="let hobby of hobbies; let i= index">{{i+1}}.{{hobby}}</li>
</ul>
```

## Events
```
<button (click)="onClick()">click me</button>
```
and then define onClick() function inside the user.ts file

## Forms
Adding a form 

```
<form (submit)="addHobby(hobby.value)">
<div>
  <label for="hobby">Hobby:</label>
  <input type="text" #hobby>
</div>
</form>

```

* Sample addHobby() definition in user.ts file

```
  addHobby(hobby){
    console.log(hobby);
    this.hobbies.unshift(hobby); // push to beginning
    return false;
  }
```

* Sample deleteHobby() can look like this

```
 deleteHobby(hobby){
    console.log(hobby);
    for(let i =0; i<this.hobbies.length;i++){
      if(this.hobbies[i] == hobby){
        this.hobbies.splice(i,1); //delete i from the index
      }
    }
  }
  
```

### ngModel

* used for binding the variables in component to its template. 
* `[()]` // indicates data binding
* [(ngModel)]="age" //bind this input to `age` property
* `name` attribute is also required for ngModel as below

```
<div>
      <label for="age">Age:</label>
      <input type="number" [(ngModel)]="age" name="age">
  </div>

```

## Services
Creating a Service
```
ng g service services/data
```

> Note:
Adds:
1. Adds `data.service.ts` file in services folder.
2. Adds the class DataService in it
3. Adds the @Injectable
Doesnt add:
1. it in app.module.ts

So we should add it in app.module.ts in
1. import {DataService} from './services/data.service'; //import statement 
2. providers: [DataService] // Services are providers

Whenever you want to use a service you have to inject as a dependency to be able to use it by using it inside a constructor

```
import {DataService}  from '../../services/data.service' 

constructor(private dataService:DataService) { ...}
```

## Http module

* import httpModule into app.module.ts
* add it to imports section

```
import {HttpModule} from '@angular/http';

imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ]

```

## Routing

*Install the router:*
* --flat flag will create it the router at root level instead of creating new file
* --module=app will add it to app.module.ts file
```
ng generate module app-routing --flat --module=app
```
```
import {RouterModule, Routes} from '@angular/router'

//create list of routes for each path
const appRoutes: Routes = [
  { path:'', component:UserComponent},
  { path:'about', component:AboutComponent}

];

// import the RouterModule & provide it the list of routes
imports: [RouterModule.forRoot(appRoutes)]

```

then inside `app.component.html`, add `<router-outlet>` where the router displays the component which matches with the route

Syntax for using the App routing module:
```
<ul>
    <li><a routerLink = "/">User</a></li>
    <li><a routerLink = "/about">About</a></li>
</ul>

```

## Observables

* Basically emit events that other things called observers can respond to .
* They allow us to do multiple actions simultaenously like promises.

* Inside the Service

```
import { map, take } from 'rxjs/operators';
import { Observable, of } from 'rxjs';

   //returns all posts as json
   getPosts():Observable<Post[]>{
    return this.http.get('https://jsonplaceholder.typicode.com/posts')
     .pipe(map(res => res.json())) 
   }

```

* then inside the user.component.ts to use the service 


```

constructor(private dataService:DataService) {  // register the service to the class
...
}

ngOnInit() { //Life cycle method
    this.dataService.getPosts().subscribe((posts) => {
      this.posts = posts;
    })
  }
  
```

## Angular in memory Web Api for mocking

*Install angular in memory web api for mocking:*
```
npm i -S angular-in-memory-web-api
```
*Install a new mock service*
```
ng generate service services/in-memory-data
```

*Import the `memory web api` & `in-memory-data` service into app.module.ts:*
```
import {HttpClientInMemoryWebApiModule} from 'angular-in-memory-web-api';
import {InMemoryDataService} from './services/in-memory-data.service';

// enable in memory web api module to use in memory data service for which mock routes are defined.
// key will be the mock route value .eg api/posts url requests will be looking for route `posts` in InMemoryDataService
imports: [
    HttpClientInMemoryWebApiModule.forRoot(InMemoryDataService, {dataEncapsulation:false})
  ]
```

*Mock InMemoryDataService:*
```
export class InMemoryDataService {

   createDb(){
     const posts = [
      {
      userId: 1,
      id: 1,
      title: "title1",
      body: "body1"
      },
      {
      userId: 1,
      id: 2,
      title: "title2",
      body: "body2"
      },
      {
      userId: 1,
      id: 3,
      title: "title3",
      body: "body3"
      }
    ];
     return { 'posts': posts };
   }
  constructor() { }
}

```
> Note: The return object key is the name of the API route (which becomes /api/posts by default), and the value is the data we want to return when the in-memory API receives a request to this route.

[more details:](https://shermandigital.com/blog/in-memory-web-api-for-testing-angular-apps/)

* To use the in memory api, we can use a PostService like below which simulates making a real http call.
* In memory Api upon looking at `api/posts` url will respond with a mock response

```
import { Injectable } from '@angular/core';
import {HttpClient, HttpHeaders} from '@angular/common/http' 
import {Post} from '../components/user/user.component'
import { Observable, of } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class PostService {
  private postsUrl = 'api/posts';
  
  constructor(private httpClient:HttpClient) {
    
   }
  
   getMockPosts():Observable<Post[]> {
    return this.httpClient.get<Post[]>(this.postsUrl)
   }
}


```
