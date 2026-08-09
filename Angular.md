**Features of Angular 17:**



1\. New Control Flow Syntax

No need for \*ngIf, \*ngFor, \*ngSwitch

Before

<div \\\\\\\*ngIf="isLoggedIn">

&#x20; Welcome

</div>



<div \\\\\\\*ngFor="let user of users">

&#x20; {{user.name}}

</div>

After

@if(isLoggedIn){

&#x20;  <h1>Welcome</h1>

}



@for(user of users; track user.id){

&#x20;  <p>{{user.name}}</p>

}



@switch(status){

&#x20;  @case('success'){

&#x20;     Success

&#x20;  }

&#x20;  @default{

&#x20;     Failed

&#x20;  }

}



2\. Better Performance

Angular optimized

Change Detection

Rendering



3\. Improved SSR (Server Side Rendering)



7\. Standalone Components by Default

No need to create modules for every component.

@Component({

&#x20;standalone:true

})



**Features of Angular 20:**

1\. Signals are Stable

Signals are Angular's modern reactive state management.

2\. Effect API Stable

Automatically execute code whenever a signal changes.

3\. linkedSignal Stable



TypeScript Code:

interface Employee {

&#x20;   id: number;

&#x20;   name: string;

}



ReplaySubject

A ReplaySubject stores previous emitted values and replays them to new subscribers.

Chat Application



2\. AsyncSubject

An AsyncSubject emits only the last value, and only after the subject completes.

File Download



@Component({

&#x20;selector:'app-home'

})

export class HomeComponent{}



Property Binding

<img \[src]="image">



3\. Event Binding

<button (click)="save()">



4\. Two-way Binding

<input \[(ngModel)]="name">

{{name}}



How Does Angular Know It Can Create the Service?

@Injectable({

&#x20;  providedIn: 'root'

})			 - Service



.subscribe(data=>{

&#x20;this.users=data;

})



10\. Routing

this.router.navigate(\['/home']);



**Dependency Injection:**

export class UserComponent {



&#x20;   constructor(private service: UserService) {



&#x20;   }



}



6\. Pipes

Pipes transform data before displaying it.

{{today | date}}



{{salary | currency}}



{{name | uppercase}}



import { Routes } from '@angular/router';

import { HomeComponent } from './home/home.component';

import { AboutComponent } from './about/about.component';

import { ContactComponent } from './contact/contact.component';



export const routes: Routes = \[



&#x20; { path: '', component: HomeComponent },



&#x20; { path: 'about', component: AboutComponent },



&#x20; { path: 'contact', component: ContactComponent }



];

<router-outlet> is a placeholder directive where Angular renders the component that matches the current route.



import { CanActivateFn } from '@angular/router';

for Guard

A route guard decides whether navigation to a route is allowed. Common guard types include:

CanActivate – Allow or block entering a route.

CanDeactivate – Prevent leaving a route (e.g., unsaved form).



To call API we need to configure provideHTTPClient provider

Inject and Import HTTPClient Service

constructor(private http: HttpClient) { }

1\. GET API

getUsers() {

&#x20; return this.http.get('http://localhost:8080/users');  - service

}



this.userService.getUsers().subscribe({  - component

&#x20; next: (data) => {

&#x20;   console.log(data);

&#x20; },

&#x20; error: (err) => {

&#x20;   console.log(err);

&#x20; }

});



2\. GET API with Path Parameter (GET /users/1)

getUser(id: number) {

&#x20; return this.http.get(`http://localhost:8080/users/${id}`);

}

this.userService.getUser(1).subscribe(data => {

&#x20; console.log(data);

});



3\. GET API with Query Parameter (GET /users?page=1)

getUsers(page: number) {

&#x20; return this.http.get(`http://localhost:8080/users?page=${page}`);

}

this.userService.getUsers(1).subscribe(data => {

&#x20; console.log(data);

});



4\. POST API (POST /users)

addUser(user: any) {

&#x20; return this.http.post('http://localhost:8080/users', user);

}

const user = {

&#x20; name: 'John',

&#x20; age: 25

};



this.userService.addUser(user).subscribe(data => {

&#x20; console.log(data);

});



5\. PUT API

updateUser(id: number, user: any) {

&#x20; return this.http.put(`http://localhost:8080/users/${id}`, user);

}

const user = {

&#x20; name: 'Peter',

&#x20; age: 30

};



this.userService.updateUser(1, user).subscribe(data => {

&#x20; console.log(data);

});



7\. API with Header

import { HttpHeaders } from '@angular/common/http';



const headers = new HttpHeaders({

&#x20; Authorization: 'Bearer token123'

});



return this.http.get('http://localhost:8080/users', { headers });



8\. API with Query Parameter + Header

import { HttpHeaders, HttpParams } from '@angular/common/http';



const headers = new HttpHeaders({

&#x20; Authorization: 'Bearer token123'

});



const params = new HttpParams()

&#x20; .set('page', '1');



return this.http.get('http://localhost:8080/users', {

&#x20; headers,

&#x20; params

});



9\. API with Request Body + Header

const headers = new HttpHeaders({

&#x20; Authorization: 'Bearer token123'

});



const body = {

&#x20; name: 'John',

&#x20; age: 25

};



return this.http.post(

&#x20; 'http://localhost:8080/users',

&#x20; body,

&#x20; { headers }

);

