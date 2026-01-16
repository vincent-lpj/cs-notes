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

## Section 5: Developer Skills & Editor Setup

#### 55. Section Intro

Take a break; How to think as a developer and how to debug code; How to set up a professional develop environment in your computer.

#### 57. Setting up Prettier and VS Code

VS Code editor

###### Extension

`Prettier`: [code formatter](https://prettier.io/), assumes how code should be like

preferences -> settings -> search `default formatter` -> select `Prettier` -> search `format on save` -> select

`.prettierrc`: change [formatter configs](https://prettier.io/docs/configuration) according to your coding style

```json
{
  "singleQuote": true,
  "arrowParens": "avoid"
}
```

`TODO Highlights`:

Code -> preference -> settings -> open settings (JSON) -> "todohighlight.isEnable": true

`Live Server` (will be introduced in next lecture):

Click `Go live` button below.

###### Auto Close Tag

Automatically add HTML/XML close tag, same as Visual Studio IDE or Sublime Text does. (Not necessary need now)

###### Auto Rename Tag

- When you rename one HTML/XML tag, automatically rename the paired HTML/XML tag

###### Snippets

Code -> Preferences -> Configure Snippets -> New Global Snippets File

```json
{
  // Place your global snippets here. Each snippet is defined under a snippet name and has a scope, prefix, body and
  // description. Add comma separated ids of the languages where the snippet is applicable in the scope field. If scope
  // is left empty or omitted, the snippet gets applied to all languages. The prefix is what is
  // used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
  // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders.
  // Placeholders with the same ids are connected.
  // Example:
  "Print to console": {
    "scope": "javascript,typescript",
    "prefix": "cl",
    "body": ["console.log();"],
    "description": "Log output to console"
  }
}
```

#### 58. Installing Node.js and Setting Up a Dev Environment

To avoid reload web broswer during development, use `Live Server` instead.

Using Live Server NPM Package in [Node.js](https://nodejs.org/en):

Node.js is a way to run JavaScript outside broswer, and some development tools.

Terminal -> New Terminal

```bash
node -v
sudo npm install live-server -g

# This will open a broswer and show index.html
live-server
```

#### 59. Learning How to Code

Set a specific, measureable, realistic and time-based goal.

Imagine a big project you want to be able to build.

Always type the code, and use it yourself.

Do not care too much about writing a clean code or efficient code.

#### 60. How to Think like a Developer: Become a Problem Solver!

Example:

Find a problem to solve:

Stay calm and slow down, do not jump into a problem without thinking:

Ask the right questions to get a clear picture of the problem.

Devide and conquer: break a big problem into smaller sub-problems

Write pseudo-code before writing the actual code.

#### 61. Using Google, StackOverflow and MDN

[StackOverflow](https://stackoverflow.com/questions)

[MDN Web Docs](https://developer.mozilla.org/en-US/)

```javascript
///////////////////////////////////////
// Using Google, StackOverflow and MDN

// PROBLEM 1:
// We work for a company building a smart home thermometer. Our most recent task is this: "Given an array of temperatures of one day, calculate the temperature amplitude. Keep in mind that sometimes there might be a sensor error."

const temperatures = [3, -2, -6, -1, "error", 9, 13, 17, 15, 14, 9, 5];

// 1) Understanding the problem
// - What is temp amplitude? Answer: difference between highest and lowest temp
// - How to compute max and min temperatures?
// - What's a sensor error? And what do do?

// 2) Breaking up into sub-problems
// - How to ignore errors?
// - Find max value in temp array
// - Find min value in temp array
// - Subtract min from max (amplitude) and return it

const calcTempAmplitude = function (temps) {
  let max = temps[0];
  let min = temps[0];

  for (let i = 0; i < temps.length; i++) {
    const curTemp = temps[i];
    if (typeof curTemp !== "number") continue;

    if (curTemp > max) max = curTemp;
    if (curTemp < min) min = curTemp;
  }
  console.log(max, min);
  return max - min;
};
const amplitude = calcTempAmplitude(temperatures);
console.log(amplitude);
```

#### 62. Debugging (Fixing Errors)

Steps:

Identify Bugs:

Find Bugs: Developer console (simple code); Debugger (complex code)

Fix Bugs:

Prevent Bugs: Writing tests using testing software

#### 63. Debugging with Console and Breakpoints

```javascript
console.log(measurement);
console.warn(measurement.type);
console.error(measurement.unit);

console.table(measurement);
```

###### Debugger in Google Chrome

Mark debug line by yourself: Sources -> breakpoints

###### Debugger statement in JavaScript

`debugger` statement

```javascript
const printForecast = function (tempArrays) {
  let forecastStr = "";
  for (let rep = 0; rep <= tempArrays.length - 1; rep++) {
    // for-loop creates a new block scope each iteration,
    // so const is not re-declared in the same scope
    const subForecastStr = `... ${tempArrays[rep]}C in ${rep + 1} days `;

    forecastStr += subForecastStr;
  }

  console.log(forecastStr);
};

const testData1 = [17, 21, 23];
const testData2 = [12, 5, -5, 0, 4];

printForecast(testData1);
printForecast(testData2);
```

#### 65. The Rise of AI Tools (ChatGPT, Copilot, Cursor AI, etc.)

The AI tools are powered by LLM.

GitHub Copilot and Cursor can use code-aware autocomplete features, and chat with you codebase.

- Make sure you 100% understand the problem. Ask questions to get a clear picture.
- Choose AI and give it a very specific prompt and enough context (language, style, etc.)
- Let AI generate the solution as code.
- Review and test the output solution. Make sure you introduce no bugs in your app.

## Section 6 [optional] HTML & CSS Crash Course

#### 68. Basic HTML Structure and Elements

`index.html`: should always be the main file of any project.

`<html></html>`: should be the root element

```html
<!-- This tells the browser that this is an HTML document -->
<html>
  <!-- The head section contains information ABOUT the page -->
  <head>
    <!-- The title appears in the browser tab -->
    <title>Learning HTML & CSS</title>
  </head>

  <!-- The body section contains everything the user sees on the page -->
  <body>
    <!-- h1 is the largest heading, usually used for the main title -->
    <h1>JavaScript is fun, but so is HTML & CSS!</h1>

    <!-- p stands for paragraph -->
    <p>You can learn JavaScript without HTML and CSS. But they are useful</p>

    <!-- h6 is the smallest heading -->
    <h6>Another Heading</h6>

    <!-- Another paragraph of text -->
    <p>Just another paragraph</p>
  </body>
</html>
```

#### 69. Attributes, Classes, and IDs

One element can be `nested` into another one, and is called `child element`.

`inline elements`

`block elements`

`openning tag`:

`closing tag`:

`Attribute`: is used to describe elements

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Learning HTML & CSS</title>
  </head>

  <body>
    <h1>JavaScript is fun, but so is HTML & CSS!</h1>
    <p class="first">
      You can learn JavaScript without HTML and CSS. But they are useful, You
      can learn more about it on
      <a
        href="https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/22648389#overview"
        >Udemy</a
      >
    </p>
    <img
      src="https://frontends.udemycdn.com/frontends-course-landing-page/_next/static/media/coding-exercises-demo-preview-desktop.6c2ffdd1.png"
    />

    <h6>Another Heading</h6>
    <p id="course-image" class="second">Just another paragraph</p>

    <form id="your-name">
      <h2>Your name here</h2>
      <p>Please fill in this form :)</p>
      <input type="text" placeholder="Your name" />
      <button>OK!</button>
    </form>
  </body>
</html>
```

Two very import attributes to identify elements.

`class`:

`id`: in convention, use dash like `course-image` to name an id.

#### 70. Basic Styling with CSS

`Selector`

- element selector
-

`<style></style>`:

`<link .../>`:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <link href="style.css" rel="stylesheet" />
  <title>Learning HTML & CSS</title>
</head>
```

###### CSS Rule Structure

```
Selector {
  Property: Value;
}
```

```css
/* ===============================
   Global styles
   =============================== */

body {
  /* Type selector (element selector)
     Applies to the <body> element */

  background-color: rgb(255, 247, 201);
  /* Non-inherited property:
     Background color does NOT inherit to child elements */

  font-family: Arial;
  /* Inherited property:
     Child elements inherit this font unless overridden */

  font-size: 20px;
  /* Inherited property:
     Child elements inherit the base font size */
}

/* ===============================
   Heading styles
   =============================== */

h1 {
  /* Type selector */

  font-size: 40px;
  /* Inherited property (but overridden here):
     Overrides the inherited font-size from body */
}

/* ===============================
   Class selector example
   =============================== */

.first {
  /* Class selector:
     Applies to any element with class="first" */

  color: red;
  /* Inherited property:
     Text color is inherited by child elements */
}

/* ===============================
   ID selector example
   =============================== */

#your-name {
  /* ID selector:
     Targets the element with id="your-name" */

  background-color: rgb(255, 220, 105);
  /* Non-inherited property */

  border: 5px solid #444;
  /* Non-inherited property:
     Borders never inherit */
}
```

#### 71. Introduction to the CSS Box Model

Box Model, along with html elements, can be checked using `inspect` in right click menu.

`content`: text, images, etc. with `width` and `height`.

`padding`: transparent area around the content, inside of the box;

`border`: goes around the padding and the content;

The areas above is called `fill area`;

`margin`: space between boxes;

## Section 7: JavaScript in the Broswer: DOM and Event [PROJECT]

#### 72. Section Intro

Finally, first project with user interface!

#### 74. PROJECT#1: Guess My Number!

###### Select HTML Elements in JavaScript

- Link JS file to the HTML

```html
<body>
  <header>...</header>
  <main>...</main>
  <script src="script.js"></script>
</body>
```

- Select and log text content to console

  `document` is the entry document to the DOM

```javascript
// Selects the first element with the class name "message" from the DOM,
// accesses its text content, and prints that text to the browser console
console.log(document.querySelector(".message").textContent);
```

#### 75. What's the DOM and DOM Manipulation

###### What is the DOM

`Document Object Model`: Connection Point between HTML and JavaScipt code

`Tree Structure`: document -> html elements (root) -> other elements

DOM methods and Properties are part of Web APIs, that can interact with JS code.

###### Manipulating Elements

```javascript
// Selects a normal HTML element (e.g. div/span) with class "score"
// and sets its text content to 10
document.querySelector(".score").textContent = 10;

// Selects an input element with class "guess"
// input elements use the "value" property instead of textContent
document.querySelector(".guess").value = 23;
```

`event`: something that happened on the page, like mouse click.

`Event Listener`: wait for some event to happen, and react to it.

`addEventListener`: a method to add an event listener to element in html. It will include an `event handler`, which is a function to react to an event.

```javascript
// document.querySelector('.check')
// → returns the first Element that matches the CSS selector ".check"

// .addEventListener('click', function () { ... })
// → registers an event listener on the element

// "click" is the event type (a string)
// function () { ... } is a function expression used as a callback
document.querySelector(".check").addEventListener("click", function () {
  // Becareful, input element should use value, instead of textContent
  const inputGuessStr = document.querySelector(".guess").value;

  if (!inputGuessStr) {
    document.querySelector(".message").textContent = "No Number Input";
  } else {
    document.querySelector(".message").textContent = inputGuessStr;
  }
});
```

#### 78. Implementing the Game Logic

Notes: It is generally good to keep state variables in your JS code, instead of relying on reading it from the DOM.

#### 79. Manipulating CSS Style

Notes:

- `style` is used to access CSS style properties
- variable used in CSS is usually like `background-color`, but camel case like `backgroundColor` should be used instead in JS
- `str` should be passed in CSS style

###### Related CSS style

```css
body {
  font-family: "Press Start 2P", sans-serif;
  color: #eee;
  background-color: #222;
  /* background-color: #60b347; */
}
```

###### JS Code

```javascript
document.querySelector("body").style.backgroundColor = "#60b347";
```
