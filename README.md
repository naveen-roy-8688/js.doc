# js.doc
# call apply bind;
```
1. call() in JavaScript
Definition

call() is a method used to invoke a function immediately while explicitly setting the value of this.
Arguments are passed individually (comma separated).

Syntax
functionName.call(thisArg, arg1, arg2, ...)

thisArg → Object that this should refer to

Remaining parameters → Arguments passed individually

Example
const person1 = {
  name: "Naveen"
};

const person2 = {
  name: "Rahul"
};

function greet(city, country) {
  console.log(`Hello ${this.name} from ${city}, ${country}`);
}

greet.call(person1, "Hyderabad", "India");
greet.call(person2, "Delhi", "India");

Output

Hello Naveen from Hyderabad, India
Hello Rahul from Delhi, India
Interview Point

call() executes the function immediately

Arguments passed individually

2. apply() in JavaScript
Definition

apply() is similar to call(), but the arguments are passed as an array.

Syntax
functionName.apply(thisArg, [arg1, arg2, ...])
Example
const person = {
  name: "Naveen"
};

function greet(city, country) {
  console.log(`Hello ${this.name} from ${city}, ${country}`);
}

greet.apply(person, ["Mumbai", "India"]);

Output

Hello Naveen from Mumbai, India
Interview Point

apply() executes immediately

Arguments passed as an array

Real Example (Very common interview example)
const numbers = [5, 10, 20, 30];

const max = Math.max.apply(null, numbers);

console.log(max);

Output

30
3. bind() in JavaScript
Definition

bind() creates a new function with this bound to a specific object, but does NOT execute immediately.

Syntax
const newFunction = functionName.bind(thisArg, arg1, arg2)
Example
const person = {
  name: "Naveen"
};

function greet(city) {
  console.log(`Hello ${this.name} from ${city}`);
}

const greetUser = greet.bind(person);

greetUser("Chennai");

Output

Hello Naveen from Chennai
Example with arguments
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);

console.log(double(5));

Output

10
Key Differences (Important for Interviews)
Feature	call()	apply()	bind()
Execution	Immediately	Immediately	Returns new function
Arguments	Passed individually	Passed as array	Passed individually
Return value	Result of function	Result of function	New function
Simple Interview Explanation (Best Answer)

call(), apply(), and bind() are used to control the value of this in JavaScript functions.

call() invokes the function immediately with arguments passed individually.

apply() invokes the function immediately but arguments are passed as an array.

bind() does not execute immediately; it returns a new function with this bound to the specified object.

```
Promises in JavaScript
Definition

A Promise in JavaScript is an object that represents the eventual completion (success) or failure of an asynchronous operation and its resulting value.

It helps handle asynchronous operations like:

API calls

File reading

Database requests

Timers

Promises help avoid callback hell and make asynchronous code cleaner and more readable.

Promise States

A Promise has 3 states:

Pending

Initial state

Operation is still running

Fulfilled (Resolved)

Operation completed successfully

Returns a result

Rejected

Operation failed

Returns an error

Example flow:

Pending → Fulfilled
Pending → Rejected
Promise Syntax
const promise = new Promise((resolve, reject) => {
   // async operation
});

resolve() → called when operation is successful

reject() → called when operation fails

Basic Example
const myPromise = new Promise((resolve, reject) => {

  let success = true;

  if (success) {
    resolve("Operation Successful");
  } else {
    reject("Operation Failed");
  }

});

myPromise
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error);
  });

Output

Operation Successful
Real Example (setTimeout)
const fetchData = new Promise((resolve, reject) => {

  setTimeout(() => {
    resolve("Data fetched successfully");
  }, 2000);

});

fetchData.then((data) => {
  console.log(data);
});

Output after 2 seconds

Data fetched successfully
Handling Errors
const checkNumber = new Promise((resolve, reject) => {

  let num = -5;

  if (num > 0) {
    resolve("Positive number");
  } else {
    reject("Negative number");
  }

});

checkNumber
  .then((result) => console.log(result))
  .catch((error) => console.log(error));

Output

Negative number
Promise Chaining (Important Interview Topic)
const promise = new Promise((resolve) => {
  resolve(10);
});

promise
  .then((num) => {
    return num * 2;
  })
  .then((num) => {
    return num * 3;
  })
  .then((result) => {
    console.log(result);
  });

Output

60
Promise Methods (Common Interview Question)
1. Promise.all()

Runs multiple promises in parallel.

Promise.all([promise1, promise2])
  .then((results) => console.log(results));

If one fails → all fail.

2. Promise.race()

Returns the first promise that completes.

Promise.race([promise1, promise2])
3. Promise.allSettled()

Returns results of all promises (success or failure).

4. Promise.any()

Returns the first successful promise.

Simple Interview Answer

You can say this in interviews:

A Promise in JavaScript is an object used to handle asynchronous operations. It represents a value that may be available now, later, or never. A Promise has three states: pending, fulfilled, and rejected. It uses .then() for success handling and .catch() for error handling, which helps avoid callback hell and makes asynchronous code more readable.

If you want, I can also explain these very important interview topics next:

Async / Await in JavaScript

Callback Hell

Event Loop

Microtask Queue vs Callback Queue

Fetch API with Promises
