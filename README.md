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
