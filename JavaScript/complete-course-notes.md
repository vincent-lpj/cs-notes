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

```javascript
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
  `${jonas.firstName} has ${jonas.friends.length} friends, and his best friend is called ${jonas.friends[0]}`,
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

#### 81. Implementing Highscores

#### 82. Refactoring Our Code: The DRY Principle

The `DRY` Principle: Do not repeat your code.

Refactor your code:

- Identify duplicate code
- create functions might be a good idea for refactoring your code.

```javascript
// for example, we can create a function to display messages
const displayMessage = function (message) {
  document.querySelector('.message').textContent = message;
};

document.querySelector('.check').addEventListener('click', function () {
  // Becareful, input element should use value, instead of textContent
  const guess = Number(document.querySelector('.guess').value);

  if (!guess) {
    // document.querySelector('.message').textContent = 'No Number Input';
    displayMessage('No Number Input');
  } else {
  ...
  }
```

#### 83. PROJECT #2: Modal Window

In this project, we will build our first UI.

Manipulating `class in HTML elements` will be learnt here.

###### Selection of DOM Elements

Usually, we store selected DOM elements in a variable, for future use.

```javascript
"use strict";

const modal = document.querySelector(".modal");
const overlay = document.querySelector(".overlay");
const btnCloseModal = document.querySelector(".close-modal");
// note that querySelector only returns the first element
// const btnOpenModal = document.querySelector('.show-modal');
// so, instead, we use querySelectorAll here
const btnOpenModal = document.querySelectorAll(".show-modal"); // return node list

console.log(btnOpenModal);

// node list can be iterated as Array do
for (let i = 0; i < btnOpenModal.length; i++) {
  console.log(btnOpenModal[i].textContent);
}
```

#### 84. Working with Classes

###### Background

Here, we interact with `classList` property in a DOM element.

Note: `classList` property contains classes that a html element belongs to, for example, `"modal hidden"` in below.

```html
<div class="modal hidden">
  <button class="close-modal">&times;</button>
  <h1>I'm a modal window 😍</h1>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
    quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
    consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
    cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
    non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </p>
</div>
<div class="overlay hidden"></div>
```

```css
/* -------------------------- */
/* CLASSES TO MAKE MODAL WORK */
.hidden {
  display: none;
}
```

###### JavaScript Code

```javascript
'use strict';

...
const closeModal = function () {
  modal.classList.add('hidden');
  overlay.classList.add('hidden');
};
const openModal = function () {
  // here, hidden class is removed from modal element,
  // so, modal does not need to follow none display in hidden class
  modal.classList.remove('hidden');
  overlay.classList.remove('hidden');
};

// node list can be iterated as Array do
for (let i = 0; i < btnOpenModal.length; i++) {
  // note that do not call the function here, use openModal, instead of openModal()
  btnOpenModal[i].addEventListener('click', openModal);
}

// when the close button is clicked, close the modal
btnCloseModal.addEventListener('click', closeModal);
// when the overlay is clicked, close the modal
overlay.addEventListener('click', closeModal);
```

#### 85. Handling an "Esc" Keypress Event

so far, we have dealt with mouse clicking event, we will learn how to deal with `keypress event`

Note that keypress event is called `global event`, because it does not belongs to any element.

Thus, the event handler function should be attached to `document` element, which is the root element of DOM.

###### Event Object

Event object will be passed in event handler function automatically as an argument.

We can catch it by `e`, `event`, or any name else.

```javascript
// listen to a keydown event, instead of click event
// we actually use keydown, instead of keypress here
document.addEventListener('keydown', function (e) {
  // the keydown event will return propery like key
  // console.log(e);
  console.log(e.key);

  // if the modal classList do not contain hidden class
  // and we press the
  if (e.key === 'Escape' && !modal.classList.contains('hidden')) {
      closeModal();
    }
  }
});
```

#### 86. PROJECT #3: Pig Game

A comprehensive project to practice all skills we have learnt in previous lectures.

```javascript
"use strict";

// Selecting elements
// # is used to select element by id, and . is for classes
const score0El = document.querySelector("#score--0");
// the following method only works for id selection
const score1El = document.getElementById("score--1");
const diceEl = document.querySelector(".dice");

// Starting conditions
score0El.textContent = 0;
score1El.textContent = 0;
diceEl.classList.add("hidden"); // be careful, it is not .hidden here

console.log(dice);
```

#### 87. Rolling the Dice

DOM elements have `classList`, `style`, `src`, etc.

```javascript
"use strict";

// Selecting elements
// # is used to select element by id, and . is for classes
const score0El = document.querySelector("#score--0");
// the following method only works for id selection
const score1El = document.getElementById("score--1");
const current0El = document.getElementById("current--0");

const diceEl = document.querySelector(".dice");
const btnNew = document.querySelector(".btn--new");
const btnRoll = document.querySelector(".btn--roll");
const btnHold = document.querySelector(".btn--hold");

// Starting conditions
score0El.textContent = 0;
score1El.textContent = 0;
diceEl.classList.add("hidden"); // be careful, it is not .hidden here

let currentScore = 0; // initialize currentScore

// console.log(dice);

// because the event handler will not be used repeatively, so use anonymous function here
btnRoll.addEventListener("click", function () {
  // 1. Generate a random dice roll
  const dice = Math.trunc(Math.random() * 6) + 1;
  console.log(dice);

  // 2. Display dice
  diceEl.classList.remove("hidden");
  diceEl.src = `dice-${dice}.png`; // select images in according to dice number

  // 3. Check for rolled 1
  if (dice !== 1) {
    currentScore += dice;
    current0El.textContent = currentScore; // change later
  } else {
    // switch to the next player
  }
});
```

#### 88. Switch the Active Player

- use `activePlayer` to hold the status of current player
- use `classList.toggle` method to add a class when absent or remove a class when exists

```javascript
"use strict";

// Selecting elements
// # is used to select element by id, and . is for classes
const player0El = document.querySelector(".player--0");
const player1El = document.querySelector(".player--1");
const score0El = document.querySelector("#score--0");
// the following method only works for id selection
const score1El = document.getElementById("score--1");
const current0El = document.getElementById("current--0");
const current1El = document.getElementById("current--1");

const diceEl = document.querySelector(".dice");
const btnNew = document.querySelector(".btn--new");
const btnRoll = document.querySelector(".btn--roll");
const btnHold = document.querySelector(".btn--hold");

// Starting conditions
score0El.textContent = 0;
score1El.textContent = 0;
const scores = [0, 0];
diceEl.classList.add("hidden"); // be careful, it is not .hidden here

let currentScore = 0; // initialize currentScore
let activePlayer = 0; // initialize player status; set default value to zero

// console.log(dice);

// because the event handler will not be used repeatively, so use anonymous function here
btnRoll.addEventListener("click", function () {
  // 1. Generate a random dice roll
  const dice = Math.trunc(Math.random() * 6) + 1;
  console.log(dice);

  // 2. Display dice
  diceEl.classList.remove("hidden");
  diceEl.src = `dice-${dice}.png`; // select images in according to dice number

  // 3. Check for rolled 1
  if (dice !== 1) {
    currentScore += dice;
    document.getElementById(`current--${activePlayer}`).textContent =
      currentScore; // change later
  } else {
    // switch to the next player
    document.getElementById(`current--${activePlayer}`).textContent = 0;
    currentScore = 0;

    activePlayer = activePlayer === 0 ? 1 : 0;

    player0El.classList.toggle("player--active"); // use toggle to dynamiclly add or remove class
    player1El.classList.toggle("player--active");
  }
});
```

#### 89. Holding the Current Score

- add a variable, `playing` , to recode the state of your game
- Make switch player code reuseable by add it to a function `switchPlayer`

```javascript
"use strict";

// Selecting elements
// # is used to select element by id, and . is for classes
const player0El = document.querySelector(".player--0");
const player1El = document.querySelector(".player--1");
const score0El = document.querySelector("#score--0");
// the following method only works for id selection
const score1El = document.getElementById("score--1");
const current0El = document.getElementById("current--0");
const current1El = document.getElementById("current--1");

const diceEl = document.querySelector(".dice");
const btnNew = document.querySelector(".btn--new");
const btnRoll = document.querySelector(".btn--roll");
const btnHold = document.querySelector(".btn--hold");

// Starting conditions
score0El.textContent = 0;
score1El.textContent = 0;
const scores = [0, 0];
diceEl.classList.add("hidden"); // be careful, it is not .hidden here

let currentScore = 0; // initialize currentScore
let activePlayer = 0; // initialize player status; set default value to zero
let playing = true;

// console.log(dice);

const switchPlayer = function () {
  document.getElementById(`current--${activePlayer}`).textContent = 0;
  currentScore = 0;

  activePlayer = activePlayer === 0 ? 1 : 0;

  player0El.classList.toggle("player--active"); // use toggle to dynamiclly add or remove class
  player1El.classList.toggle("player--active");
};

// because the event handler will not be used repeatively, so use anonymous function here
btnRoll.addEventListener("click", function () {
  // run the code below only when playing
  if (playing) {
    // 1. Generate a random dice roll
    const dice = Math.trunc(Math.random() * 6) + 1;
    console.log(dice);

    // 2. Display dice
    diceEl.classList.remove("hidden");
    diceEl.src = `dice-${dice}.png`; // select images in according to dice number

    // 3. Check for rolled 1
    if (dice !== 1) {
      currentScore += dice;
      document.getElementById(`current--${activePlayer}`).textContent =
        currentScore; // change later
    } else {
      // switch to the next player
      switchPlayer();
    }
  }
});

btnHold.addEventListener("click", function () {
  // only active when playing!
  if (playing) {
    // 1. add current score to active player's score
    scores[activePlayer] += currentScore;

    // 2. check if player's score is >= 100
    document.getElementById(`score--${activePlayer}`).textContent =
      scores[activePlayer];

    // finish the Game
    if (scores[activePlayer] >= 20) {
      playing = false; // deactive the game
      diceEl.classList.add("hidden");

      document
        .querySelector(`.player--${activePlayer}`)
        .classList.add("player--winner"); // define winner style in css and attached here to player block

      document
        .querySelector(`.player--${activePlayer}`)
        .classList.remove("player--active");
    } else {
      // switch to another user
      switchPlayer();
    }
  }
});
```

#### 90. Resetting the Game

- summarize init codes into `init` function
- call init function at the very beginning, and when that button is pressed

```javascript
"use strict";

// Selecting elements
// Note that querySelector requires a query
// # is used to select element by id, and . is for classes
const player0El = document.querySelector(".player--0");
const player1El = document.querySelector(".player--1");
const score0El = document.querySelector("#score--0");
const score1El = document.getElementById("score--1"); // this method only works for id selection
const current0El = document.getElementById("current--0");
const current1El = document.getElementById("current--1");

const diceEl = document.querySelector(".dice");

const btnNew = document.querySelector(".btn--new");
const btnRoll = document.querySelector(".btn--roll");
const btnHold = document.querySelector(".btn--hold");

// declare variables before init function alter them
let scores, currentScore, activePlayer, playing;

const init = function () {
  // Starting conditions
  score0El.textContent = 0;
  score1El.textContent = 0;
  current0El.textContent = 0;
  current1El.textContent = 0;

  diceEl.classList.add("hidden"); // be careful, it is not .hidden here

  player0El.classList.remove("player--winner"); // note that it will not return error when it does not exist
  player0El.classList.add("player--active"); // default player should be player 0;
  player1El.classList.remove("player--winner");
  player1El.classList.remove("player--active");

  // initializing variables
  scores = [0, 0];
  currentScore = 0; // initialize currentScore
  activePlayer = 0; // initialize player status; set default value to zero
  playing = true;

  document.getElementById("score--0").textContent = 0;
  document.getElementById("score--1").textContent = 0;
  document.getElementById("current--0").textContent = 0;
  document.getElementById("current--1").textContent = 0;
};

const switchPlayer = function () {
  document.getElementById(`current--${activePlayer}`).textContent = 0;
  currentScore = 0;

  activePlayer = activePlayer === 0 ? 1 : 0;

  player0El.classList.toggle("player--active"); // use toggle to dynamiclly add or remove class
  player1El.classList.toggle("player--active");
};

// init the game when beginning
init();

// because the event handler will not be used repeatively, so use anonymous function here
btnRoll.addEventListener("click", function () {
  // run the code below only when playing
  if (playing) {
    // 1. Generate a random dice roll
    const dice = Math.trunc(Math.random() * 6) + 1;
    console.log(dice);

    // 2. Display dice
    diceEl.classList.remove("hidden");
    diceEl.src = `dice-${dice}.png`; // select images in according to dice number

    // 3. Check for rolled 1
    if (dice !== 1) {
      currentScore += dice;
      document.getElementById(`current--${activePlayer}`).textContent =
        currentScore; // change later
    } else {
      // switch to the next player
      switchPlayer();
    }
  }
});

btnHold.addEventListener("click", function () {
  // only active when playing!
  if (playing) {
    // 1. add current score to active player's score
    scores[activePlayer] += currentScore;

    // 2. check if player's score is >= 100
    document.getElementById(`score--${activePlayer}`).textContent =
      scores[activePlayer];

    // finish the Game
    if (scores[activePlayer] >= 100) {
      playing = false; // deactive the game
      diceEl.classList.add("hidden");

      document
        .querySelector(`.player--${activePlayer}`)
        .classList.add("player--winner"); // define winner style in css and attached here to player block

      document
        .querySelector(`.player--${activePlayer}`)
        .classList.remove("player--active");
    } else {
      // switch to another user
      switchPlayer();
    }
  }
});

// initiaie the condition when this button is pressed
btnNew.addEventListener("click", init);
```

## Section 8 How JavaScript Works Behind the Scenes

#### 91. Section Intro

Learn how the language works

#### 93. An High-Level Overview of JavaScript

###### Extension of Definition

Definition in previous sections:

> JavaScript is a high-level, object-oriented, multi-paradigm, programming language.

Definition now:

> JavaScript is a high-level, prototype-based, object-oriented, multi-paradigm, interpreted or just-in-time compiled, dynamic, single-threaded, garbage-collected programming language with first-class functions and a non-blocking event loop concurrency model.

###### Nine Topics of JavaScript

`High Level`:

Low-level, like C, will directly manipulate resources, like computer memory.

High-level, like JS and Python, have abstractions, but is lower than C.

`Garbage Collection`:

A algrhthim that cleans unused objects.

`Interpreted or just-in-time compiled`:

1. Every program that computer can execute is machine code, include only 0 and 1.
2. JS code should, eventually, converted to machine code, by `interpreting` or `compiling`.
3. In JS, this progress happens in JavaScript engine.

`Multi-Paradigm`:

Paradigm is an approach and mindset of structuring code, which will direct your coding style and technique.

1. Procedual Programming
2. Object-oriented programming (OOP)
3. Functional programming

`Prototype-based object-oriented`:

Almost everything in JS is object, like an Array.

Array has methods, which is stored in blueprints, called `prototype`. This will be `inherited` and used in any array.

`First-class functions`:

Functions are treated as `variables`, which can be stored and passed.

```javascript
// Here, function closeModal is passed as an argument in another function
overlay.addEventListener("click", closeModal);
```

`Dynamic`:

In JS, we do not assign data types to variables, instead, it is only known when JS engine execute code.

`Single-threaded` and `Non-blocking event loop`:

Concurrency Model: how JS engine handles multiple tasks happening at the same time.

JavaScript runs in one single thread.

#### 94. The JavaScript Engine and Runtime

###### JavaScript Engine

JS Engine is simply a program that executes JavaScript code.

Every broswer has a JavaScript Engine, like V8 Engine in Google Chrome.

###### Components of JavaScript Engine

`Call Stack`: where your code is executed.

`Heap`: where objects are stored.

###### How JavaScript Engine Works

Compilation vs. Interpretation

`Compilation`: Entire code is converted into `machine code` at once, and written to a binary file that can be executed by a computer.

`Interpretation`: Interpreter runs through the source code and executes it `line by line`.

How JS does:

`Just-in-time compilation`: Entire code is converted into machine code at once, and then execute it `immediately`, without generating a binary file.

source code -> parsing -> compilation -> execution

compiled code is optimized and swapped during execution

###### JavaScript Runtime

JS runtime is like a container that contains everything you need to run JS code, with the core of JS engine.

`Runtime in Browser`:

includes JavaScript Engine, Web APIs (DOM, etc), callback queue (such as functions in event listener).

#### 95. Execution Contexts and The Call Stack

###### Sample Code

```javascript
// this is a line of top-level code
const name = 'John';

// const first = () is also top-level code, but not the function body
const first = () => {
  let a = ;
  const b = second(7,9);
  a = a + b;
  return a;
}

// function second(x,y) is top-level code
function second(x,y) {
  var c = 2;
  return c;
}

// this is a line of top-level code
const x = first();
```

###### Execution of JavaScript Code

(complication) -> Execution includes three steps:

1. Creation of `global execution context` (for top-level code);
   - `top-level code` is code that outside any function
   - function body are only executed when they are called
2. Execution of top-level code inside global execution context;
3. Execution of `functions` and waiting for callbacks;

###### Execution Context

Execution context is environment in which a piece of JavaScript is executed. It stores all necessary information for some code to be executed.

Components

- Variable Environment
  - let, const, and var declaration
  - Functions
  - `argument` object

- Scope chain
- `this` keyword

Notes: arrow function do not have `argument` object and `this` keyword

###### Execution Contexts of Code Sample

In the sample above, three execution contexts will be created during execution.

- Global
  - Includes name, first, second, and x
- first()
  - Includes a and b
  - do not include arguments because of arrow function
- second()
  - Includes c
  - Includes `arguments = [7. 9]`

###### Call Stack

To keep track of execution context, `call stack` is introduced.

`Call Stack` is basically execution contexts is stacked during execution.

In call stack, each execution context is stacked in order, and poped out when finishing.

In sample code, the call stack is like, from top to bottom, `second() -> first() -> global`;

#### 96. Scope and The Scope Chain

`Scope Chain` is contained in every execution context.

The most important questions that scoping answers:

**Where do variables live, and where can we access a certain variable, and where not**

###### Scope Concept

- `Scoping`: How our variables are organized and accessed.
- `Lexical Scoping`: Scoping is controlled by **placement** of functions and blocks in the code.
  - for example, inner functions can always access variables from their outer scopes.
- `Scope`: Space or environment in which a certain variable is **declared** (variable environment in case of functions)
  - `global` scope
  - `function` scope
  - `block` scope
- `Scope of variables`: Region of our code where a certain variable can be **accessed**.

###### The 3 Types of Scope

1. Global Scope
   - global scope is outside of any function block

   - variable declared in global scope can be accessed **everwhere**

     ```javascript
     const me = "Jona";
     ```

2. Function Scope
   - Variable are accessible only inside function, NOT outside

   - Also called local scope

     ```javascript
     function calcAge(birthYear) {
       const now = 2037;
       const age = now - birthYear;
       return age;
     }

     console.log(now); // Illegal; ReferenceError
     ```

3. Block Scope (ES6)
   - Variables are accessible only **inside block** (block scoped).

   - However, this only applies to **let** and **const** variables.

   - Functions are also block scoped (only in strict mode).

     ```javascript
     if (year >= 1981) {
       const millenial = true;
       const food = "Avacado toast";
     }

     console.log(millenial); // Illegal, ReferenceError
     ```

###### The Scope Chain

Scope has access to variables from all **outer** scopes.

The following scopes are chained, in which inner scope can access variables in outer scopes

​ global scope <- first() scope <- second() scope

However, outer scope can never have access to inner scopes.

For example, in global scope, you can not access variables that are stored in first() scope.

###### Code Analysis

Note that scope is only about where the function is placed, instead of called.

```javascript
"use strict";

const a = "Jonas";
// Function declarations are hoisted,
// so they can be called before they are defined
first();

function first() {
  const b = "Hello!";
  second();

  function second() {
    const c = "Hi";
    // note here althrough function third is called here,
    // it can not access variable c;
    third();
  }
}

function third() {
  const d = "Hey";
  // console.log(d + c + b + a);
  // ReferenceError: c, b is not defined
  console.log(d + a);
}
```

**Image of Scope Chain**

global scope <- first() scope <- second scope

​ <- third() scope

**Breakdown of Scope Chain**

1. Global Scope
   - a = 'Jonas'
   - first = <function>
   - third = <function>
2. first() scope
   - b = 'Hello!'
   - second = <function>
   - access to global scope
     - a = 'Jonas'
     - first = <function>
     - third = <function>
3. second() scope
   - c = 'Hi'
   - access to first() scope
     - b = 'Hello!'
     - second = <function>
   - access to global scope
     - a = 'Jonas'
     - first = <function>
     - third = <function>
4. third() scope
   - d = 'Hey'
   - access to global scope
     - a = 'Jonas'
     - first = <function>
     - third = <function>

**Conclusion**

Therefore,

- first and second function can be called before it is defined.
- third function can only have access to variables d and a.

#### 97. Scoping in Practice

```javascript
"use strict";

function calcAge(birthYear) {
  const age = 2037 - birthYear;
  // When firstName is not found in calcAge() scope
  // JS will do a variaable look-up
  // and find it in global scope
  console.log(firstName);

  function printAge() {
    // When JS engine can not find age in printAge() scope
    // it will look up at its parent scope, calcAge() scope

    // firstName variable is find in global scope
    const output = `${firstName}, You are ${age}, born in ${birthYear}.`;
    console.log(output);

    if (birthYear >= 1981 && birthYear <= 1996) {
      var millenial = true;

      // It is legal to have variabes that have the same name in different scope
      // However, if you change variables in outer scopes, the value will changes
      const firstName = "Steven";
      // JS will use 'Steven' instead of 'Jonas',
      // because it can be found in this scope, JS engine will not look it up in global scope.
      const messageStr = `Oh, and you're a millenial ${firstName}`;
      console.log(messageStr);
    }

    // messageStr is block scoped, and can be accessed only in if blocks
    // ReferenceError
    // console.log(messageStr);

    // however, var can not be block scoped
    console.log(millenial);
  }

  printAge();
  return age;
}

// Although firstName is defined after calcAge function, it will work
const firstName = "Jonas";
calcAge(1991);

// Global scope can not access variable in its child scope, calcAge() scope
// ReferenceError
// console.log(age);
// printAge();
```

#### 98. Variable Environment: Hoisting and The TDZ

###### Hoisting

Hoisting means to make some type of variables accessible/usable in the code before they are actually declared. So, it seems like that variables are lifted to the top of their scope.

Behind the scenes, before execution, code is scanned for variables declarations, and for each variable, a new property is created in the variable environment object.

|                                | Hoisted?     | Initial Vale         | Scope    |
| ------------------------------ | ------------ | -------------------- | -------- |
| function declaration           | yes          | actual function      | block    |
| var variables                  | yes          | undefined            | function |
| let, const variables           | no (part of) | <uninitialized>, TDZ | block    |
| function expression and arrows |              |                      |          |

- You can call a function defined by function declarations before the code block, because of hoisting.
- The hoisting of `var` variables is weird, so that is why you should keep using `let` and `const` variables.
- The behavior of function expression and arrows is dependent on `var`, `let` and `const` in front of it.

###### Temporal Dead Zone: let and const

```javascript
"use strict";

const myName = "Jonas";

if (myName === "Jonas") {
  // -----------TDZ for job variables-------------
  // Uncaught ReferenceError: Cannot access 'job' before initialization
  console.log(`Jonas is a ${job}`);
  const age = 2037 - 1991;
  console.log(age);
  // ---------------------------------------------

  const job = "teacher";

  // Uncaught ReferenceError: x is not defined
  console.log(x);
}
```

Note: calling a variable defined by `let` and `const`, before it is declared, and without declarations, will cause different kinds of error.

#### 99. Hoisting and TDZ in Pratice

Note:

- Although function declarations can be hoisted, it is a good idea to use function after it is defined.
- Do not use `var` to declare variables, use `let` and `const` instead.
- Variables created by `var` will create a property in `window` object.

```javascript
"use strict";

// Variables

// will log undefined
// because me variable defined by var is hoisted
console.log(me);

//Uncaught ReferenceError: Cannot access 'job' before initialization
//because this line is located in TDZ of job variable
// console.log(job);

// Uncaught ReferenceError: Cannot access 'year' before initialization
// same as job
// console.log(year);

var me = "Jonas";
let job = "teacher";
const year = 1991;

// Functions
// will log 5, because function defined by delaration is hoisted
console.log(addDecl(2, 3));

// Uncaught ReferenceError: Cannot access 'addExpr' before initialization
// Same as variables, because it is defined by const
// console.log(addExpr(2, 3));

// Uncaught TypeError: addArrow is not a function
// It is hoisted, because it is defined by var,
// however, because undefined is not function, it can not be called here.
console.log(addArrow(2, 3));

// Function Declaration
function addDecl(a, b) {
  return a + b;
}

// Function Expression
const addExpr = function (a, b) {
  return a + b;
};

// Arrow Function
var addArrow = (a, b) => a + b;
```

#### 100. The this Keyword

`this` keyword/variable is special variable that is created for every <u>execution context</u> (every function).

- `this` keyword is one of the three components of execution context.
- It takes the value of (points to) the 'owner' of the function in which `this` keyword is used.
- It is not static. It depends on how the function is called, and the value is **only assigned** when the function is **called**.

|                        | Meaning of `this`                              |
| ---------------------- | ---------------------------------------------- |
| Method                 | Object that is calling the method              |
| Simple function call   | undefined                                      |
| Arrow function         | The parent's `this`, because it has not `this` |
| Event Listener         | DOM element that the handler is attached to    |
| new, call, apply, bind | ... later in the lecture                       |

#### 101. The this Keyword in Practice

`window` is the global object, so, `this` in global scope will point to window.

```javascript
"use strict";

// window
console.log(this);

const calcAge = function (birthYear) {
  const age = 2037 - birthYear;

  // this keyword is undefined in regular function
  // undefined will be logged here
  console.log(this);
  return age;
};

// This functiion call has no owner
calcAge();

const calcAgeArrow = (birthYear) => {
  const age = 2037 - birthYear;

  // this keyword points to window
  // because in arrow function, lexical this is applied
  console.log(this);
  return age;
};

// Arrow Function is called
calcAgeArrow();

const jonas = {
  birthYear: 1991,
  calcAge: function () {
    // In a method call, jonas object is returned by this
    // jonas is the owner of this
    console.log(this);
    console.log(this.birthYear);
  },
};

jonas.calcAge();
```

```javascript
// Method Browing
matilda.calcAge = jonas.calcAge;

// Beaware, this in this function call will present matilda,
// because matilda is the owner of this function
matilda.calcAge();

const normalFunc = jonas.calcAge;
// this in normalFunc is undefiend, because the owner becomes a normal function
normalFunc();
```

#### 102. Regular Functions vs. Arrow Functions

- Never use arrow functions as an object method, because `this` in arrow functions inside an object will return `window` object in global scope, instead of the object it belongs to.
- But, arrow function works amazingly as nested function in object method, because `this` keyword will be inherited from its parent.

```javascript
"use strict";

const jonas = {
  firstName: "Jonas",
  birthYear: 1991,
  calcAge: function () {
    console.log(2037 - this.birthYear);

    // Using regular function in a method will make this keyword invalid
    // Because this keywory in a regular function is undefined.
    // Uncaught TypeError: Cannot read properties of undefined (reading 'birthYear')
    // const isMillenial = function () {
    //   console.log(this);
    //   console.log(this.birthYear >= 1981 && this.birthYear <= 1996);
    // };

    // Instead, use arrow function when you want to nest a function in a method
    // Because this keyword in an arrow function will return its parent's this
    const isMillenial = () => {
      console.log(this);
      console.log(this.birthYear >= 1981 && this.birthYear <= 1996);
    };
    isMillenial();
  },

  greet: () => {
    // Here, this keyword will return windoe, which is this keyword in global scope
    // Because this keyword in arrow function will return its parent's this
    console.log(this);
    // There is no firstName property in window,
    // So, undefined will be returned
    console.log(`Hey, ${this.firstName}`);
  },
};

jonas.calcAge();
jonas.greet();
```

###### Arguments Keyword

`arguments` keyword only exist in regular functions, which are defined by function declaration and expression, NOT in arrow functions.

#### 103. Memory Management: Primitives vs. Objects

`Memory Management` refers how JS engine allocates places for variables, and free up that memory space when these variables are not needed.

###### Life Cycle

Every value in JS goes through a life cycle

1. Allocate Memory
2. Use Memory
3. Release Memory

###### Allocate Memory

Values in JS belong to either `primatives` or `objects`

`HEAP` is one of two parts of JavaScript Engine, where objects are stored.

`Call Stack` is where functions run, and where primatives, and **references to objects** stored.

###### Understanding Object Reference

```javascript
const name = 'Jonas';
// primative values are stored directly in execution context
const age = 46;
let newAge = age;
// note here age is still 46
// but newAge becomes 47
newAge++;

// objects are stored in HEAP
// in execution context, only reference to objects are stored
const location = {
  city = 'Faro';
  country = 'Portugal';
}
const newLocation = location;
// because location and newLocation stores reference to the same object
// both object that locatin and newLocation refers to are changed
// the values of property location.city and newLocation.city both become 'Lisbon'
newLocation.city = 'Lisbon'
```

#### 104. Object Reference in Practice (Shallow vs. Deep Copies)

```javascript
"use strict";

// the following object, jessica, is stored in the HEAP of JS engine
// and the call stack will hold a reference to the memory address to which the object is stored in HEAP
const jessica = {
  firstName: "Jessica",
  lastName: "Williams",
  age: 27,
};

// when we tried to copy the object jesscia
// we did not create a new object in the HEAP
// only the reference to the same object are shared
const marriedJessica = jessica;
// that is why we can change an object declared by const
// in fact, we did not change reference itself, but only the object it points to
marriedJessica.lastName = "Davis";
// JS engine will return error if we change the reference stored in jessica, which is declared by const
// Uncaught TypeError: Assignment to constant variable.
// jessica = { x: 23 };

// note: in function, only reference of object is passed as argument
const marryPerson = function (originalPerson, newLastName) {
  // thus, the original object stored in HEAP is changed, instead of creating a new object
  originalPerson.lastName = newLastName;
  return originalPerson;
};

// so, the objects inside and outside the function will be changed, because they are actually the same one
const marriedJessicaFunc = marryPerson(jessica, "Davis");

// both lastName of jessica and marriedJessica will be changed
console.log("Before", jessica);
console.log("After", marriedJessica);
console.log("After (func):", marriedJessicaFunc);
```

###### Shallow Copy

```javascript
"use strict";

const jessica = {
  firstName: "Jessica",
  lastName: "Williams",
  age: 27,
  // note that family also only hold reference to the array object
  // so shallow copy only copy the reference to the array
  family: ["Alice", "Bob"],
};

// Shallow Copy
// here, ... copies the object jessica, and store it in the HEAP
// and the new object's reference is stored in jessicaCopy
// however, this shallow copy has some shortcomings
const jessicaCopy = { ...jessica };
jessicaCopy.lastName = "Davis";

console.log("Before:", jessica);
console.log("After:", jessicaCopy);

jessica.family.push("John");

// change in family array applies to both jessica, and jessicaCopy
console.log("Before:", jessica);
console.log("After:", jessicaCopy);
```

###### Deep Copy (Clone)

```javascript
"use strict";

const jessica = {
  firstName: "Jessica",
  lastName: "Williams",
  age: 27,
  // note that family also only hold reference to the array object
  family: ["Alice", "Bob"],
};

// Deep Copy
const jessicaClone = structuredClone(jessica);
jessicaClone.lastName = "Davis";
jessicaClone.family.push("John");

// note that the object of jessica and jessicaCLone are different now
console.log(jessica);
console.log(jessicaClone);
```

#### 105. Memory Management: Garbage Collection

Here we focus on the third phrase of memory life cycle: `Release Memory`

Question: How memory free up after we no longer need a value

- Call Stack: variable environment is simply deleted when EC pops off stack
  - Since global execution context always exist, global variables will be in call stack forever
- HEAP: `Garbage Collection`
  - Garbage Collection is automatical, and can not be controlled by users.
  - `mark-and-sweep` algorithm.

`Memory Leak` refers to when objects that are no longer needed are **incorrectly** still reachable, and therefore not being garbage collected.

###### Future Topics

- Closure -> a closer look at functions
- Prototypal Inheritance -> OOP with JavaScript
- Event Loop -> Asynchronous JavaScript
- How the DOM Really Works -> Advanced DOM and Events

## Section 9: Data Structures, Modern Operators, and Strings

#### 106. Section Intro

Continue learning JS syntax, with focus on data structure.

#### 108. Destructing Arrays

`Destructing` means breaking data structures down into smaller data structures.

We use `[]` to destructure arrays.

Because arrays are ordered, variable order matters during destruction.

```javascript
// without destructure
const arr = [2, 3, 4];
const a = arr[0];
const b = arr[1];
const c = arr[2];

// destructure the array
const [x, y, z] = arr;
```

```javascript
const restaurant = {
  name: "Classico Italiano",
  location: "Via Angelo Tavanti 23, Firenze, Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian", "Organic"],
};

// elements can be skipped by lefting a space in between
// const [first, second] = restaurant.categories;
let [main, , secondary] = restaurant.categories;
console.log(main, secondary);
```

###### Swap Values by Destructure

```javascript
[secondary, main] = [main, secondary];
console.log(main, secondary);
```

###### Destructure Array Returned by Function

```javascript
const restaurant = {
  ...
  starterMenu: ['Focaccia', 'Bruschetta', 'Garlic Bread', 'Caprese Salad'],
  mainMenu: ['Pizza', 'Pasta', 'Risotto'],
  order: function (starterIndex, mainIndex) {
    return [this.starterMenu[starterIndex], this.mainMenu[mainIndex]];
  },
  ...
}

// receieve two values from function call
const [starter, mainCourse] = restaurant.order(2, 0);
console.log(starter, mainCourse);
```

###### Nested Destructuring

```javascript
const nested = [2, 4, [5, 6]];
const [i, , [j, k]] = nested; // JS will automatically unfold this
console.log(i, j, k);
```

###### Default Values in Destructuring Arrays

This technique is helpful when dealing with APIs, to avoid getting `undefined`

```javascript
const [p = 1, q = 1, r = 1] = [8, 9];
console.log(p, q, r);
```

#### 110. Destructuring Object

We use `{}` to destructure object.

Because order does not matter, we should destructure object using its `property names`.

```javascript
const { name, openingHours, categories } = restaurant;
console.log(name, openingHours, categories);
```

###### Change Variable Names

We can also have a different variable name here. Using `:`.

```javascript
const {
  name: restaurantName,
  openingHours: hours,
  categories: tags,
} = restaurant;

console.log(restaurantName, hours, tags);
```

###### Default Values in Destructuring Object

```javascript
const { menu = [], starterMenu: starters = [] } = restaurant;
console.log(menu, starters);
```

###### Mutating Variables

```javascript
let a = 111;
let b = 999;
const obj = { a: 23, b: 7, c: 24 };
// {a, b} = obj will not work, because {} represents a code block
({ a, b } = obj);
console.log(a, b);
```

###### Nested objects

```javascript
const openingHours = {
  thu: {
    open: 12,
    close: 22,
  },
  fri: {
    open: 11,
    close: 23,
  },
  sat: {
    open: 0, // Open 24 hours
    close: 24,
  },
};

const {
  fri: { open: o, close: c },
} = openingHours;

console.log(o, c);
```

###### Destructuring Object in Function Arguments

```javascript
const restaurant = {
...
  // destructure object passed as argument here
  // with default values
  orderDelivery: function ({ starterIndex = 1, mainIndex =0, time, address }) {
    console.log(
      `Order receieved!
      ${this.starterMenu[starterIndex]} and ${this.mainMenu[mainIndex]}
      will be delivered to ${address} and ${time}`,
    );
  },
};

// Prepare object that will be passed into function here
const foodOrder1 = {
  time: '22:30',
  address: 'Via del Sole, 21',
  mainIndex: 2,
  starterIndex: 2,
};

restaurant.orderDelivery(foodOrder1); // here pass one object only
```

#### 111. The Spread Operator (...)

`Spread Operator` takes all elements individually from the old array.

It is useful when

- shallow copies
- creating new array
- Pass elements into a function

```javascript
const arr = [7, 8, 9];
// Imagine that we would like to make a new array base on arr, with 1 and 2 at the beginning
const badNewArr = [1, 2, arr[0], arr[1], arr[2]];
console.log(badNewArr);

const goodNewArr = [1, 2, ...arr];
const copyNewArr = [...arr];
console.log(goodNewArr);
console.log(copyNewArr);

// It is also useful if we would like to pass elements into a fuction individually
console.log(...arr);
```

Spread operator has two forms:

1. `Iterable spread` (e.g. [...iterable]) — requires an iterable (arrays, strings, maps, sets).
2. `Object spread` (e.g. {...obj}) — works on plain objects by copying enumerable properties.

###### Iterable Spread

```javascript
// Iterables: arrays, strings, maps, sets, NOT objects
const str = "Jones";
const letters = [...str];
console.log(letters);
```

###### Passing Arguments using Iterable Spread

```javascript
const restaurant = {
  orderPasta: function (ing1, ing2, ing3) {
    console.log(`Here is your delicious pasta with ${ing1}, ${ing2}, ${ing3}`);
  },
};

const ingredents = ["a", "b", "c"];
restaurant.orderPasta(...ingredents);
```

###### Object Spread

```javascript
const RestaurantCopy = { ...restaurant };
const newRestaurant = { ...restaurant, founder: "Guiseppe" };
```

#### 112. Rest Pattern and Parameters

`Rest Pattern` does the opposite of spread operator. It is to pack elements into an array.

- Note, the rest element should be the last element
- Rest Pattern works in destructuring an array

###### Rest Pattern in Array

```javascript
// SPREAD, because on the RIGHT side of =
const arr = [1, 2, ...[3, 4]];

// REST, because on the LEFT side of =
const [a, b, ...others] = [1, 2, 3, 4, 5];

// other = [3, 4, 5]
console.log(arr, a, b, others);
```

###### Rest Pattern in Object

```javascript
const { sat, ...weekdays } = restaurant.openingHours;
console.log(sat, weekdays);
```

###### Rest Pattern in Function

```javascript
const add = function (...numbers) {
  let sum = 0;
  for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
  }
  console.log(sum);
};

add(2, 3, 5);

// Rest works as the opposite of spread
const newNumbers = [2, 3, 5];
add(...newNumbers);
```

#### 113. Short Circuiting (&& and ||)

Logic operators have been used in boolean values, however, they can alos used in `non-boolean` values.

###### &&

```javascript
// use in ANY datatype, and return ANY datatype
// shortciruiting of || will return the first truthy value, or the last falsy value if all values are falsy
console.log(3 || "Jones");
console.log("" || "Mike");
console.log(undefined || 0 || "" || "Hello" || 23 || null); // will return 'Hello'
```

- It is useful when we want to set a default value but not sure about ig it is absent

```javascript
const restaurant = {};

const guest1 = restaurant.numGuests || 10; // here, restaurant.numGuests is undefined, so 10 is returned
console.log(guest1);
```

###### ||

```javascript
// shortciruiting of && will return the first falsy value, or the last truthy value if all values are true
console.log(0 && "Jonas"); // will return 0
console.log(7, "Jonas"); // will return 'Jonas'

console.log("Hello" && 23 && null && "Jonas"); // will return null
```

```javascript
// Practical Examples
if (restaurant.orderPizza) {
  restaurant.orderPizza();
}

// The if statement can be replaced by this line below
restaurant.orderPizza && restaurant.orderPizza(); // only executed when restaurant has the property of orderPizza
```

######

#### 114. The Nullish Coalescing Operator (??)

`Nullish value` is basically falsy values without 0 and ''.

```javascript
const restaurant = {
  numGuests: 0,
};

// Here, we want to set a default value of 10, when the property of numGuest does not exist
// However, shortcircuiting of || can not do this job

// || shortciruiting
const guest1 = restaurant.numGuests || 10; // will return 10, which we do not want

// Nullish: null and undefined (NOT 0 or '')
const guest2 = restaurant.numGuests ?? 10; // will return 0
console.log(guest1, guest2);
```
