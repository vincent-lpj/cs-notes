## Section 2: JavaScript Fundamentals - Part1

[The Complete JavaScript Course 2025: From Zero to Expert](https://www.udemy.com/course/the-complete-javascript-course/)

[Course Source Code](https://github.com/jonasschmedtmann/complete-javascript-course)

#### 6. Hello World

###### Developer Tools

command + option + J

Use developer tools' console to type JavaScript in `Console`

```javascript
alert("Hello World!");

let js = "amazing";
if (js === "amazing") alert("JavaScript is fun!");
console.log(40 + 8 + 23 - 10);
```

#### 7. A Brief Introduction to JavaScript

###### Definition

JavaScript is a high-level, object-oriented, multi-paradigm programming language.

###### Cores of Web Development

HTML, CSS and JavaScript

content, presentation, and dynamic effects

###### Frameworks

Browser; Web Servers (node.js); Native Mobile Apps; Native Desktop Apps;

modern JS after ES2015

#### 8. Linking a JavaScript File

Inline script

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>JavaScript Fundamentals – Part 1</title>
    <style>
        body {
          height: 100vh;
      ...
    </style>
    <script>
      let js = "amazing";
      if (js === "amazing") alert("Javascript is fun");
      40 + 8 + 23 - 10;
      console.log(40 + 8 + 23 - 10);
    </script>
  </head>
  <body>
    <h1>JavaScript Fundamentals – Part 1</h1>
  </body>
</html>
```

script.js

    <script src="script.js"></script>

#### 11. Data Types

values: object or primitive

`dynamic typing`, do not declare variable types

###### Variables

camelCase

store value to variables

###### Primitive Data Types

Number; String; Boolean; Undefined; Null; Symbol; BigInt;

Unlike Python, number in JS contains only float type numbers.

```javascript
let js = "amazing";
console.log(40 + 8 + 23 - 10);

console.log("Jonas");
console.log(23);

let firstName = "Matilda";

console.log(firstName);
console.log(firstName);
console.log(firstName);
```

###### Comment

```javascript
//write your comment here

/*
your 
multiline
comment
*/
```

#### 12. let, const and var

###### Declaring Varables

let: used to declare variables that will change.

const: always use const,

Variables defined by const can not be empty or changed.

Notes: use const as much as possible unless you are sure that this variable will change; Never use var.

var: legacy items

#### 13. Basic Operators

Operators allows us to translate or combine values.

Operators inclues:

Basic operators; Assignment operators, Coparison operators.

```javascript
+ - * / ** =
let x = 10 + 5;
x += 10;
x *= 4;
// means x = x + 1
x ++;
console.log(x);
```

conbine string

```
const firstName = "Jonas";
const lastName = "Schmedtmann";
console.log(firstName + " " + lastName);
```

#### 14. Operator Precedence

mdn operator precendence

```
let x, y;
// Firstly, basic operator, then, assignment operator
x = y = 25 - 10 - 5;
console.log(x, y);
```

#### 17 String and Template Literals

```javascript
const firstName = "Jonas";
const job = "teacher";
const birthYear = 1991;
const year = 2037;

//
const jonas =
  "I'm " + firstName + ", a " + (year - birthYear) + "year's old " + job + "!";
console.log(jonas);

// Template Literals
// `${var}`
const jonasNew = `I'm ${firstName}, a ${year - birthYear} years's old ${job}!`;
console.log(jonasNew);

const multiLines = `This 
is 
a
String!`;
console.log(multiLines);
```

#### 18. Taking Decisions: if / else Statements

if/else control structures

```javascript
const age = 19;
const isOldEnough = age >= 18;

if (isOldEnough) {
  console.log("Sarah can start driving license 🚗");
} else {
  const year = 18 - age;
  console.log(`Sarah is too young, wait for ${year} years.`);
}

const age = 18;
// {} can be omitted when there is only one line
if (age === 18) console.log("You just bacame an audult");
```

#### 20. Type Conversion and Coercion

Type conversion is manually convert from type to type.

Type Coercion is JS convert types for us.

```javascript
// Type conversion
const inputYear = "1991";
console.log(Number(inputYear), inputYear);

console.log(Number(inputYear) + 18);

// Will return a NaN (invalid number)
console.log(Number("Jonas"));
console.log(typeof NaN);

console.log(String(23), 23);

// Type coersion
console.log("I'm " + 23 + " years old");
console.log("23" - "10" - 3);
// Type is converted weirdly
console.log("23" + "10" + 3);
```

#### 21. Truthy and Falsy Values

Five falsy values: 0, '', undefined, null, NaN

Except false itself, these falsy values will be seen as false in judgement

```javascript
const money = 0;
if (money) {
  console.log("Don't spend it all");
} else {
  console.log("You should get a job");
}

let height;
if (height) {
  console.log("YAY! Height is defined");
} else {
  console.log("Height is UNDEFINED");
}
```

#### 22. Equality Operators

```
// strict equality operators: ===
// always use === in use
const age = 18;
if (age === 18) console.log("You just bacame an audult");

// loose equality operators: ==
// Type coersion enabled
if (age == "18") console.log("You just bacame an adult (loose)");
```

#### 23 & 24. Boolean Logic and Logical Operators

The `AND`, `OR` & `NOT` operators

`&&`, `||`, and `!`

```javascript
const hasDriversLicense = true;
const hasGoodVision = true;
console.log(hasDriversLicense && hasGoodVision);
console.log(hasDriversLicense || hasGoodVision);
console.log(!hasDriversLicense);

const isTired = true;
if (hasDriversLicense && hasGoodVision && !isTired) {
  console.log("Sarah is able to drive");
} else {
  console.log("Someone else should drive");
}
```

#### 26. The switch Statement

```javascript
const day = "wednesday";
switch (day) {
  case "monday": // day === 'monday'
    console.log("Plan course structure");
    console.log("Go to coding meetup");
    break;
  case "tuesday":
    console.log("Prepare theory videos");
    break;
  case "wednesday":
  case "thursday":
    console.log("Write code examples");
  case "friday":
    console.log("Record videos");
  case "saturday":
  case "sunday":
    console.log("Enjoy the weekend :D");
    break;
  default:
    console.log("Not a valid day!");
}
```

#### 27. Expression and Statement

`Expression`: produce values, smaller

`Statement`: convey actions, larger

```javascript
// Expressions
3 + 4;
1991;
true && false && !false;
// Statements
if (23 > 10) {
  const str = "23 is bigger";
}
```

#### 28. The Condition Operator

Operator always produce a value, so it is an expression

```javascript
// Using condition operator to assign value
const age = 23;
const myDrink = age >= 18 ? "wine" : "water";
console.log(myDrink);

// Alternative way to assign value
let mySecondDrink;
if (age >= 18) {
  mySecondDrink = "wine";
} else {
  mySecondDrink = "water";
}
console.log(mySecondDrink);

// Usage in Template Literals
console.log(`I would like to drink ${age >= 18 ? "wine" : "water"}`);
```

#### 30. JavaScript Release: ES5, ES6+ and ESNext

During Development: Simply use the latest Google Chrome!

During Production: Use Babel to transpire and polyfill your code.

`ES5`: fully supported in all browsers (down to IE 9 from 2011)

`ES6` and later: will be supported in all modern browsers, but not older browsers

In this course, modern JavaScript will be tought in this course.

## Section 3 JavaScript Fundamentals - Part2

#### 32. Activating Strict Mode

secure JavaScript code

`use strict` should always be used at the beginning of the JS file

This course will always use strict mode in the following sections.

```javascript
// should be at the begining of the code
// it forbid us to do certain things, and will create visible errors
"use strict";

let hasDriversLicense = false;
const passTest = true;

// Introduce an error on perpose
// Strict mode will expose this error will others will fail silently.
if (passTest) hasDriverLicense = true;
if (hasDriversLicense) {
  console.log("I can drive");
}

// Attempt to use reserved word
const interface = "Audio";
```

#### 34. Functions

a piece of code that can be reused.

`function` keyword is used when defining a function.

`return` keyword will return a value when function is called.

invoke function, call function or run function

```javascript
// Defining the function
function logger() {
  console.log("My name is Jones");
}

// Invoking the function
logger();

// Defining function with parameters
function fruitProcessor(apples, oranges) {
  console.log(apples, oranges);
  const juice = `Juice with ${apples} apples and ${oranges} oranges.`;
  return juice;
}

// The actural value put into parameters are arguments
const appleJuice = fruitProcessor(5, 0);
const appleOrangeJuice = fruitProcessor(2, 4);
console.log(appleJuice);
console.log(appleOrangeJuice);
```

#### 35. Function Declarations vs. Expressions

function declarations

using `function` keyword to define a function

```javascript
// Function Declaration
const age1 = calcAge1(1991); // function defined by declaration can be called before definition

function calcAge1(birthYear) {
  return 2037 - birthYear;
}

// Function Expression
const calcAge2 = function (birthYear) {
  return 2037 - birthYear;
};

const age2 = calcAge2(1991);
console.log(age1, age2);
```

#### 36. Arrow Functions

Arrow functions are one simpler form of function declarations

```javascript
// Function Expression
const calcAge2 = function (birthYear) {
  return 2037 - birthYear;
};

const age2 = calcAge2(1991);
console.log(age1, age2);

// Arrow Functions with one parameter
const calcAge3 = (birthYear) => 2037 - birthYear;
const age3 = calcAge3(1991);
console.log(age3);

// Arrow Functions with multi-line
const yearsUntilRetirement = (birthYear, firstName) => {
  const age = 2037 - birthYear;
  const retirement = 65 - age;
  const message = `${firstName} will be retired in ${retirement} years`;
  return message; // return keyword is needed for multi-line function
};
console.log(yearsUntilRetirement(1991, "John"));
```

#### 37. Function Calling other Functions

```javascript
function cutFruitPieces(fruit) {
  return fruit * 4;
}

function fruitProcessor(apples, oranges) {
  // apples will replace parameters of fruits here
  const applePieces = cutFruitPieces(apples);
  const orangePieces = cutFruitPieces(oranges);

  const juice = `Juice with ${applePieces} pieces of apple and ${orangePieces} pieces of oranges`;
  return juice;
}

// 2 will replace the parameter of apples and 3 for orange parameter
console.log(fruitProcessor(2, 3));
```

#### 38. Reviewing Functions

Function Review: 3 different function types

- `Function Delaration`

- `Function Expression`

- `Arrow Function`: Great for a quick one-line functions

```javascript
// Funtion Name: calcAge
// Parameters: birthYear, firstName
// placeholders to receive input values, like local variables of a function
function calcAge(birthYear, firstName) {
  // Function Body:
  // block of code
  const age = 2037 - birthYear;
  console.log(`${firstName} is ${age} years old`);

  // return statement to output a value from the function and terminate execution
  return age;
}

// Arguments: 1991, "Jonas"
// actual values of functions parameters, to input data
// Calling, running or invoking the function by ()
// use variable, age, to save returned value(function output)
const age = calcAge(1991, "Jonas");
```

#### 40. Introduction to Arrays

Two most important `data structures` in JS are `Arrays` and `Objects`.

```javascript
// creating array using literals
const friends = ["Michael", "Steven", "Peter"];
console.log(friends);

// creating array using Array function
const years = new Array(1991, 1984, 2000, 2020);
console.log(years);

// element 0
console.log(friends[0]);
// length property of array
console.log(friends.length);
// mutate one element in an array
// Note: array is mutable even if decleared with const
friends[2] = "Jay";
console.log(friends[2]);

// array is very flexible
const firstName = "Jonas";
const jonas = [firstName, "Schndman", 2037 - 1991, friends];
console.log(jonas);
```

#### Basic Array Operations (Methods)

`push`: attach an element at the end of an array

`unshift`: attach an element at the beginning of an array

`pop`: remove and return the last element of an array

`shift`: remove and return the first element of an array

`indexOf`: return the index of an element

`includes`: return if an element exists in an array

```javascript
// add elements
const friends = ["Michael", "Steven", "Peter"];
friends.push("Jay");
console.log(friends);


friends.unshift("John");
console.log(friends);

// remove elements
fconst lastElement = friends.pop();  // pop method will return the popped element
console.log(friends);
console.log(lastElement);

const firstElement = friends.shift();
console.log(friends);
console.log(firstElement);

// find the index of a specific element
const indexSteven = friends.indexOf("Steven");
console.log(friends);
console.log(indexSteven);

// find out if Bob exist in this array
const isBobExist = friends.includes("Bob");
console.log(friends);
console.log(isBobExist);  // will return false
```

#### 43. Introduction to Objects

Elements in an array can not be referenced by name, instead, they can only be referenced by index.

To solve this problem, `Object` is introduced.

Object groups variables together which really belong to each other.

The `order` of elements in an object is not relevant, it is unstructured data.

```javascript
// use curl braces to create an object
// Object literal syntax
const jonas = {
  firstName: "Jonas",
  lastName: "Schmedmann",
  age: 2037 - 1991,
  job: "teacher",
  friends: ["Micheal", "Peter", "Steven"],
};

console.log(jonas);
```

#### 44. Dot vs. Bracket Notation

```javascript
// Dot Notation
console.log(jonas.lastName);

// Bracket Notation
console.log(jonas["lastName"]);

const nameKey = "Name";
console.log(jonas["last" + nameKey]); // the advantage of bracket notation is that it can have exprssions

// Operator Precendence: mdn operator precendence
// the dot notation (Member access) has a higher priority over {}
console.log(
  `${jonas.firstName} has ${jonas.friends.length} friends, and his best friend is called ${jonas.friends[0]}`
);
```

```javascript
// Object can add elements by dot and bracket notations
jonas.location = "Portugal";
jonas["twitter"] = "test twitter addresses";

console.log(jonas);
```

#### 45. Object Method

```javascript
const jonas = {
  firstName: "Jonas",
  lastName: "Schmedmann",
  birthYear: 1991,
  job: "teacher",
  friends: ["Micheal", "Peter", "Steven"],
  hasDriverLisence: true,

  // function expression returns a value, so this value can be stored in an object
  // calcAge: function (birthYear) {
  //   return 2037 - birthYear;
  // }

  // this represents jonas object here
  //   calcAge: function () {
  //     console.log(this);
  //     return 2037 - this.birthYear;
  //   },
  // };

  calcAge: function () {
    this.age = 2037 - this.birthYear;
    return this.age;
  },
};

// console.log(jonas.calcAge(1991));
// since this is used, there is not need to put argument here
console.log(jonas.calcAge());

// the value of calcAge function has been stored in age property
console.log(jonas.age);
```

#### 47. Iteration: The for Loop

`Control Structure` inclues not only if/else, but also `for loop`.

```javascript
// for loops keeps running when condition is true
// Counter Variable declaration； Conditional expression； Update expression
for (let rep = 1; rep <= 10; rep++) {
  // Block statement (loop body)
  console.log(`Lifting weight repetition ${rep}`); // Template literal (string interpolation)
}
```

#### 48. Looping Arrays, Breaking and Continuing

```javascript
const jonasArray = [
  "Jonas",
  "Schmedtmann",
  2037 - 1991,
  "teacher",
  ["Michael", "Peter", "Steven"],
  true,
];

// Constant variable declaration
// - An empty array literal used for collecting values
const typesArray = [];

for (let i = 0; i < jonasArray.length; i++) {
  console.log(jonasArray[i], i, typeof i);

  typesArray.push(typeof jonasArray[i]);
}

console.log(typesArray);
```

`continue`: exit the current iteration of this loop and start the next one.

`break`: completly terminiate the whole loop.

```javascript
// continue and break
console.log("---CONTINUE---");
for (let i = 0; i < jonasArray.length; i++) {
  if (typeof jonasArray[i] !== "string") continue;

  typesArray.push(typeof jonasArray[i]);
}

console.log("---BREAK---");
for (let i = 0; i < jonasArray.length; i++) {
  if (jonasArray[i] === 46) break;

  typesArray.push(typeof jonasArray[i]);
}

console.log(typesArray);
```

#### 49. Looping Backwards and Loops in Loops

```javascript
const jonasArray = [
  "Jonas",
  "Schmedtmann",
  2037 - 1991,
  "teacher",
  ["Michael", "Peter", "Steven"],
  true,
];

for (let i = jonasArray.length - 1; i >= 0; i--) {
  console.log(i, jonasArray[i]);
}
```

```javascript
for (let exercise = 1; exercise < 4; exercise++) {
  console.log(`----${exercise}----`);
  // inner loops
  for (let rep = 1; rep < 6; rep++) {
    console.log(`Lifting weight repetition ${rep}`);
  }
}
```

#### 50. The while Loop

```javascript
// counter is declared outside of while loop
let rep = 1;

// only condition can be declared in while loop
while (rep <= 10) {
  console.log(`Lifting weight repetition ${rep}`);
  rep++;
}
```

## Section 4: How to Navigate This Course

#### 53. Pathways and Section Roadmaps

This course is a complete JavaScript course, so it is lengthy.

`Section Roadmap` tells you which part is essential, and which one is not.
