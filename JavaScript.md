**JavaScript:**

JavaScript is a high-level, dynamically typed, interpreted programming language mainly used to make web pages interactive and dynamic.

It can run in:

Browsers — Chrome, Firefox, Edge, etc.

Servers — using environments like Node.js

Other environments such as mobile/desktop applications



JavaScript is synchronous by default, but it supports asynchronous operations. (single-threaded)

Code executes one statement at a time, in order.

JavaScript can perform operations without blocking the rest of the program.

it supports asynchronous programming through mechanisms such as callbacks, Promises, async/await, Web APIs, and the event loop.



var - used to assign variables in javascripts, can be reassigned, Function-scoped

var name = "Lawrence";

name = "John";

console.log(name);



let - Use let when the value needs to change.It is block-scoped:

let count = 1;

count = 2; // Allowed

if (true) {

&#x20;   let x = 10;

}

console.log(x); // Error



const - Use const when the variable should not be reassigned.

const pi = 3.14;

const objects can still change

const prevents reassignment



Data Types:

let name = "Lawrence";    // String

let age = 25;            // Number

let active = true;       // Boolean

let x;                   // Undefined

let y = null;            // Null



let arr = \[1, 2, 3];     // Array

let obj = {name: "John"}; // Object



== vs ===

console.log(5 == "5"); ->true

Because == performs type conversion.

=== checks both:

value

type



Function:

function add(a, b) {

&#x20;   return a + b;

}



console.log(add(10, 20));

Normal function:

Callback function

A callback function in JavaScript is a function that is passed as an argument to another function and is called later.

function greet(name) {

&#x20;   console.log("Hello " + name);

}

function process(callback) {

&#x20;   callback("Lawrence");

}

process(greet);



numbers.forEach(n => {

&#x20;   console.log(n);

});

const result = numbers.map(n => n \* 2);

const sum = numbers.reduce((total, n) => {

&#x20;   return total + n;

}, 0);



Objects:

Object destructuring is a convenient way to extract properties from an object and store them in variables.

const user = {

&#x20;   name: "John",

&#x20;   age: 25,

&#x20;   city: "Mumbai"

};

const { name, age } = user;

console.log(name); // John

console.log(age);  // 25



Spread operator:

const a = \[1, 2, 3];

const b = \[...a, 4, 5];

console.log(b);

Output -> \[1, 2, 3, 4, 5]



Optional chaining:

const employee = {

&#x20;   address: {

&#x20;       city: "Mumbai"

&#x20;   }

};

console.log(employee.address?.city); -> Mumbai if city is null it will give undefined



Nullish coalescing:

const name = null;

console.log(name ?? "Unknown");



**Hoisting:**

console.log(a);

var a = 10;

undefined



Global scope -> Variable declared outside the function

Function scope -> Inside the function

Block scope -> within a particular block (if)



Closure:

function outer() {



&#x20;   let count = 0;



&#x20;   return function inner() {

&#x20;       count++;

&#x20;       console.log(count);

&#x20;   };

}



const counter = outer();



counter();

counter();

counter();

Because the inner function remembers the variable count from its outer function.



async/await is built on top of Promises.

A Promise represents a value that will be available now, later, or never.

A Promise has three states:

Pending → operation is still running

Fulfilled → operation completed successfully

Rejected → operation failed



async is used before a function to make that function return a Promise.

async function greet() {

&#x20;   return "Hello";

}



greet().then((result) => {

&#x20;   console.log(result);

});

await is used to wait for a Promise to settle and get its result.

It can normally be used inside an async function.

async function getData() {

&#x20;   const result = await promise;



&#x20;   console.log(result);

}

