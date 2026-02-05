###### Reference

[FastAPI - The Complete Course 2026 (Beginner + Advanced)](https://www.udemy.com/course/fastapi-the-complete-course/)

## Section 1: Introduction

#### 1. Introduction

Learning to build **RESTful** and **full-stack** application using **fastapi**.

Not only to teach how to build fastapi application, but also knowledges about full-stack development.

**No** fastapi knowledge is needed to start this course.

#### 2. Course Content

###### Learning Path / Roadmap

Phase 1: Foundations

- Introduction
- Python Refresher

Phase 2: Backend Projects

- Project 1 (Restful API endpoint)
- Project 2 (Class & Error Handling)
- Project 3 (Database & ORM)

Phase 3: Core Features

- Authentication (JWT)
- Routing

Phase 4: Advanced Backend

- Project 3.5 (DB & DB Migration)
- Project 4 (Unit & Integration Testing)

Phase 5: Full Stack

- Project 5 (Full Stack Development)

Phase 6: Tooling & Workflow

- Git / GitHub Setup
- Development

#### 3. How to Get Most

[FastAPI - The Complete Course](https://github.com/codingwithroby/fastapi-the-complete-course)

## Section 2: Python Installation & Refresher

#### 42. Object Oriented Programming in Python

```python
# Define a class named Enemy
class Enemy:
    # Type annotation: this attribute should be a string
    type_of_enemy: str

    # Class attribute: default health points for all Enemy objects
    health_points: int = 10

    # Class attribute: default attack damage for all Enemy objects
    attack_damage: int = 1


# Create an instance (object) of the Enemy class
enemy = Enemy()

# Assign a value to the instance attribute type_of_enemy
enemy.type_of_enemy = 'Zombie'

# Print the enemy's information using an f-string (formatted string)
print(f"{enemy.type_of_enemy} has {enemy.health_points} health points and can do attack of {enemy.attack_damage}")
```

#### 43. Abstraction in Python Overview

###### What is Abstraction?

`Abstraction` means to hide the implementation and only show necessary details to the user.

Let us think of flashlight, it has a 'on' and 'off' switch, you will have a beam of light when turning the 'on' switch.

You do **NOT** need to know the light inside the flashlight, you only focus on the switch

###### Example

In `Enemy.py`, we define:

```python
# Define a class named Enemy
class Enemy:
    type_of_enemy: str
    health_points: int = 10
    attack_damage: int = 1

    def talk(self):
      print("I am an enemy!")
```

Then, in the `main.py` file (just like the flashlight):

```python
from Enemy import *

enemy = Enemy();
enemy.talk()  # Here, we only need to focus on calling talk method, instead of caring about what is inside

# I am an enemy!
```

###### Why Use Abstraction?

- This allow users to not have to understand what the functionality is behind the scenes
- You can create simple and reusable code
- Allows for a Better use of the DRY principle (Do not repeat your self)
- Enables Python object to be more scalable

#### 44. Abstraction in Python

###### Example

In `enemy.py`, we define:

Then we have three functionalities in our Enemy class.

```python
class Enemy:
    # Type annotation: enemy type should be a string
    type_of_enemy: str
    # Default health points (class attribute)
    health_points: int = 10
    # Default attack damage (class attribute)
    attack_damage: int = 1

    def talk(self):
        print(f"I am a {self.type_of_enemy}. Be prepared to fight!")

    def walk_forward(self):
        print(f"{self.type_of_enemy} moving forward to you")

    # Define an instance method for attacking
    def attack(self):
        print(f"{self.type_of_enemy} attacks for {self.attack_damage} damage")
```

In `main.py`, we can call the function (method).

```python
# Import the Enemy class from enemy.py
from enemy import Enemy

# Create an Enemy object
zombie = Enemy()
# Initialize the attribute 'type_of_enemy'
zombie.type_of_enemy = 'Zombie'

# Call the attack method
zombie.attack()
```

#### 45. Constructors in Python Overview

`Constructor` is used **create** and **initialize** and object of a class with or without starting values.

```python
# Example of calling a constructor
enemy = Enemy()
```

###### Different Types of Constructors

- Default / Empty Constructors (Do nothing)
- No Argument Constructors
- Parameter Constructors

###### Default / Empty Constructor

`self` refers to the current class/object.

```python
class Enemy:
    type_of_enemy: str
    health_points: int = 10
    attack_damage: int = 1

    # Automatically created if no constructor is found
    # Run when enemy = Enemy()
    def __init__(self):
        pass

    def talk(self):
        print(f"I am a {self.type_of_enemy}. Be prepared to fight!")
```

###### No Argument Constructor

```python
class Enemy:
    type_of_enemy: str
    health_points: int = 10
    attack_damage: int = 1

    # No argument is needed when initiating an object
    # Will print "New enemy created!" when executing enemy = Enemy()
    def __init__(self):
        print("New enemy created!")

    def talk(self):
        print(f"I am a {self.type_of_enemy}. Be prepared to fight!")
```

###### Parameter Constructor

This is the most popular constructor

```python
class Enemy:
    # Constructor method: runs automatically when a new object is created
    def __init__(self, type_of_enemy: str, health_points: int = 10, attack_damage: int = 1):
        # Initialize the enemy type (instance attribute)
        self.type_of_enemy = type_of_enemy
        # Initialize health points with a default value
        self.health_points = health_points
        # Initialize attack damage with a default value
        self.attack_damage = attack_damage

    # Instance method: makes the enemy speak
    def talk(self):
        # Print a message using formatted string (f-string)
        print(f"I am a {self.type_of_enemy}. Be prepared to fight!")

```

```python
# Create an Enemy object using default values
# health_points = 10, attack_damage = 1 (default parameters)
enemy = Enemy("Zombie")

# Create a new Enemy object with custom values
# health_points = 15, attack_damage = 3 (override default parameters)
# This line will overwrite the previous enemy object
enemy = Enemy("Zombie", 15, 3)
```

#### 46. Constructor in Python

Instance attributes can be reassigned after an object is created.
In some cases, this is not safe, so we use **encapsulation** to control access.

```python
# Create an Enemy object
zombie = Enemy("Zombie", 1, 10)

# Reassign the attribute directly (not safe)
zombie.type_of_enemy = "Ogre"

# Print the modified attribute
print(zombie.type_of_enemy)
# Output: Ogre
```

#### 47. Encapsulation in Python Overview

`Encapsulation` means bundling of data.

Suppose we do not want the type of enemy to be able to change.

###### Getters & Setters

## Section 3: FastAPI Overview

#### 61. FastAPI Overview

`FastAPI` is a Python web-framework for building mordern RESTful APIs.

[Official Documentation](https://fastapi.tiangolo.com/)

- Few Bugs
- Quick & Easy
- Robust
- Standard

###### Where Does FastAPI Fit with An Application Architecture?

A webpage communicates with a backend server through HTTP APIs (often RESTful).

FastAPI can also render webpage, and create full-stack application.

```
Web Page  <------------    Fast API
           ------------>    Server
```

## Section 4: FastAPI Setup & Installation

#### 62. Virtual Environment Overview

A virtual environment is a Python environment that is **isolated** from those in other Python environments.

###### How to Install Dependencies

`pip` is the Python package manager, it is used to install and update packages.

Python has already has an included dependency for virtual environments called `venv`.

```bash
python -m pip --version
# pip 24.0 from ...
```

#### 64. FastAPI and Virtual Environment Installation (Mac)

Creating a virtual environment for our FastAPI application.

- pip3 → system Python
- pip → current environment

```bash
pip3 list
# Show all Python packages installed globally

mkdir fastapi
# Create a new folder named "fastapi" for the project

cd fastapi
# Enter the project directory

python3 -m venv fastapienv
# Create a virtual environment named "fastapienv"

source fastapienv/bin/activate
# Activate the virtual environment

# (fastapienv) xxx@xxx will appear in the terminal
# This means the virtual environment is now active

pip list
# Show all Python packages installed in the virtual environment
```

```bash
pip install fastapi
pip install "uvicorn[standard]"
```

## Section 5: Part 1 - FastAPI Request Method Logic

#### 65. Books Project Introduction

We are going to have a look at basic HTTP request methods.

###### What will We Create?

- Creating and enhancing books to learn the basics of FastAPI
  - Include CRUD Operations: Create, Read, Update and Delete

###### Request and Response

Webpage request data from FastAPI server using **[HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)**.

```
             Response
Web Page  <------------    Fast API
           ------------>    Server
             Request
```

HTTP Request Method has its own verbs for CURD operation.

| CRUD   | HTTP Request Method |
| ------ | ------------------- |
| Create | POST                |
| Read   | GET                 |
| Update | PUT                 |
| Delete | DELETE              |

#### 66. Download Source Code

[FastAPI: The Complete Course](https://github.com/codingwithroby/fastapi-the-complete-course)

#### 67. GET Request Method Overview

###### Outline of FastAPI Application

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/api-endpoint")
async def first_api():
    return {"message": "Hello Eric!"}
```

###### Dive In

`async` stands for asynchronous. It allows non-blocking execution,
so the server can handle multiple requests efficiently.

```python
# 127.0.0.1:8000/api-endpoint
# Localhost address to access the API endpoint
# 127.0.0.1 means "this computer"
# 8000 is the port number
# /api-endpoint is the route path


# Add an API endpoint using a decorator
# @app.get() specifies the HTTP method and URL path

@app.get("/api-endpoint")
async def first_api():
    # This function handles requests to /api-endpoint
    # It returns JSON data to the client
    return {"message": "Hello Eric!"}
```

###### Run FastAPI Application

`uvicorn` is the web server we use to start a FastAPI application

```bash
# Start the FastAPI application using Uvicorn
# books       → Python file name (books.py)
# app         → FastAPI instance inside books.py
# --reload    → Automatically restart the server when code changes
#              (for development only)

uvicorn books:app --reload
```

```
INFO:     Will watch for changes in these directories: ['/***/fastapi']
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [*****] using WatchFiles
INFO:     Started server process [*****]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

#### 68. Create FastAPI Endpoint

(Same as above)

#### 69. FastAPI Project: Enhance Get Request

###### Adjustment

We want our API endpoint to return a list of books.

```python
from fastapi import FastAPI

app = FastAPI()

BOOKS = [
    {'title': 'Title One', 'author': 'Author One', 'category': 'science'},
    {'title': 'Title Two', 'author': 'Author Two', 'category': 'science'},
    {'title': 'Title Three', 'author': 'Author Three', 'category': 'history'},
    {'title': 'Title Four', 'author': 'Author Four', 'category': 'math'},
    {'title': 'Title Five', 'author': 'Author Five', 'category': 'math'},
    {'title': 'Title Six', 'author': 'Author One', 'category': 'math'},
]

@app.get("/books")
async def read_all_books():
    return BOOKS
```

###### Automatic docs

`127.0.0.0.1:8000/docs`

`/docs` is the central page for viewing and testing FastAPI APIs (Swagger UI). It is used to view and test APIs in the browser.

- Show all API endpoints
- Display HTTP methods (GET, POST, etc.)
- Show request parameters
- Display response formats
- Allow online API testing

#### 70. FastAPI Project: Path Parameters Overview

###### What are Path Parameters

`Path Parameters` are request parameters that have been attached to the URL.

- usually defined as a way to find information based on location

###### Example

```python
# {dynamic_param} is a path parameter (dynamic value in the URL)
@app.get("/books/{dynamic_param}")
# This function receives the value from the URL path
async def read_all_books(dynamic_param: str):
    return {"dynamic_param": dynamic_param}
```

Request:

```
http://localhost:8000/books/macbeth
-> {"dynamic_param":"macbeth"}
```

#### 71. FastAPI Project: Path Parameters

###### Real Example

```python
@app.get("/books/{book_title}")
async def read_book(book_title:str):
    for book in BOOKS:
        if book.get('title').casefold() == book_title.casefold():
            return book
```

Request:

In URL, `%20` means space.

```
http://localhost:8000/books/title%20four
-> {"title":"Title Four","author":"Author Four","category":"math"}
```
