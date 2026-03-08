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
Callback Hell

Async / Await

Event Loop

Microtask Queue vs Callback Queue

I'll explain them simply with theory + examples.

1. Callback Hell
Definition

Callback Hell happens when multiple asynchronous operations are nested inside callbacks, making the code hard to read and maintain.

This creates a pyramid structure.

Example
setTimeout(() => {
  console.log("Step 1");

  setTimeout(() => {
    console.log("Step 2");

    setTimeout(() => {
      console.log("Step 3");
    }, 1000);

  }, 1000);

}, 1000);

Structure becomes like:

setTimeout
   └── setTimeout
        └── setTimeout
Problem

Hard to read

Hard to debug

Hard to maintain

Solution

Use:

Promises

Async/Await

2. Async / Await
Definition

async/await is a modern way to handle promises, making asynchronous code look like synchronous code.

Rules

async → makes a function return a Promise

await → waits for a Promise to resolve

Example with Promise
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Data received");
    }, 2000);
  });
}

async function getData() {
  const result = await fetchData();
  console.log(result);
}

getData();

Output after 2 seconds

Data received
Error Handling
async function getData() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.log(error);
  }
}
3. Event Loop (Very Important Interview Topic)
Definition

The Event Loop is a mechanism that allows JavaScript to perform non-blocking asynchronous operations even though JavaScript is single-threaded.

It manages execution between:

Call Stack

Web APIs

Callback Queue

Microtask Queue

Flow
Call Stack → Web APIs → Callback Queue → Event Loop → Call Stack
Example
console.log("Start");

setTimeout(() => {
  console.log("Timer");
}, 0);

console.log("End");

Output

Start
End
Timer
Why?

Because:

setTimeout goes to Web API

Then to Callback Queue

Event Loop executes it after call stack is empty

4. Microtask Queue vs Callback Queue

This is a very common interview question.

Callback Queue (Macrotask)

Contains:

setTimeout

setInterval

DOM events

setImmediate

Example:

setTimeout(() => {
  console.log("Timeout");
}, 0);
Microtask Queue

Contains:

Promise .then()

catch()

finally()

queueMicrotask()

MutationObserver

Example:

Promise.resolve().then(() => {
  console.log("Promise");
});
Important Rule

Microtask Queue executes BEFORE Callback Queue

Interview Example
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");

Output

Start
End
Promise
Timeout

Execution Order:

Call Stack → Microtask Queue → Callback Queue
Best Short Interview Explanation

You can say this:

JavaScript is single-threaded but handles asynchronous operations using the Event Loop. The Event Loop manages tasks between the Call Stack, Web APIs, Microtask Queue, and Callback Queue. Promises and async/await help avoid callback hell and make asynchronous code more readable. Microtasks like Promise callbacks execute before macrotasks like setTimeout.
