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

#### 72. FastAPI Project: Quert Parameters Overview

###### What are Query Parameters

`Query paremeters` are request parameters (`name=value `pairs) that have been attched after a "?".

Examples:

URL:

```
127.0.0.1:8000/books/?category=math
```

#### 73. FastAPI Project: Query Parameters

Query parameters are used to **filter** data, based on the url provided.

```python
# Unlike path parameters, query parameters do not need to be written in the URL path
# Request URL Example: localhost:8000/books/?category=science
@app.get("/books/")
async def read_book_by_query(category: str):
    books_to_return = []
    for book in BOOKS:
        if book.get("category").casefold() == category.casefold():
            books_to_return.append(book)

    return books_to_return
```

#### 74. FastAPI Project: Post Request Overview

###### POST HTTP Requet Method

- Used to **create new data** on the server

- POST requests can include a **request body**, which allows sending additional data

- The request body is usually sent in **JSON format**

  ```json
  { "title": "Title Seven", "author": "Author Two", "category": "math" }
  ```

`Body()` is used to **explicitly declare a request body parameter** in FastAPI.
It tells FastAPI that the data should be read from the **HTTP request body**, not from query parameters or the URL path.

#### 75. FastAPI Project: Post Request

POST is the `Create` method. So we will use POST method to add new data into our book list.

```python
from fastapi import Body

# Create a POST endpoint to add a new book
@app.post("/books/create_book")
async def create_book(new_book = Body()):

    # Get the JSON data from the request body
    # and store it in the variable "new_book"

    # Add the new book to the BOOKS list
    BOOKS.append(new_book)

    # Return the created book to the client
    return new_book
```

###### Test

We can also test this endpoint by Swagger UI at `/docs`

```bash
curl -X 'POST' \
  'http://localhost:8000/books/create_book' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{"title": "Title Seven", "author": "Author Two", "category": "math"}'
```

#### 76. FastAPI Project: Put Request Overview

###### PUT Request Method

- Used to **update** data

- PUT can have a body that has additional information (like POST) that GET does not have

  ```json
  { "title": "Title Six", "author": "Author Two", "category": "science" }
  ```

- We can get the body by `Body()` as well

#### 77. FastAPI Project: Put Request

Use `PUT` method to update a book or change some information about the book

```python
from fastapi import Body

# Create a PUT endpoint to update an existing book
@app.put("/books/update_book")
async def update_book(updated_book = Body()):

    # Loop through all books using index
    for i in range(len(BOOKS)):

        # Compare titles (case-insensitive) to find the target book
        if BOOKS[i].get("title").casefold() == updated_book.get("title").casefold():

            # Replace the old book with the new data
            BOOKS[i] = updated_book

            # Return the updated book
            return updated_book

    # If no book is found, return an error message
    return {"message": "Book not found"}
```

###### Test

```bash
curl -X 'PUT' \
  'http://localhost:8000/books/update_book' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{"title": "Title Six", "author": "Author Two", "category": "science"}'
```

#### 78. FastAPI Project: Delete Request Overview

###### DELETE Request Method

- Used to **delete** data from the server
- Usually removes a resource by **ID or unique field** (such as title)
- Most DELETE requests use **path parameters** to identify the target
- Does not usually contain a request body

#### 79. FastAPI Project: Delete Request

```python
# Create a DELETE endpoint to remove a book by title
@app.delete("/books/delete_book/{book_title}")
async def delete_book(book_title: str):

    # Loop through all books using index
    for i in range(len(BOOKS)):

        # Compare titles (case-insensitive) to find the target book
        if BOOKS[i].get("title").casefold() == book_title.casefold():

            # Remove the matched book from the list
            BOOKS.pop(i)

            # Stop the loop after deleting one book
            break

    # Return a success message
    return {"message": "Book deleted (if it existed)"}
```

###### Test

```python
curl -X 'DELETE' \
  'http://localhost:8000/books/delete_book/Title%20Four' \
  -H 'accept: application/json'
```

###### API Reference Table

| Method | Endpoint                     | Function                |
| ------ | ---------------------------- | ----------------------- |
| GET    | `/books`                     | Get all books           |
| GET    | `/books/{title}`             | Get book by title       |
| GET    | `/books/?category=`          | Get books by category   |
| POST   | `/books/create_book`         | Create a new book       |
| PUT    | `/books/update_book`         | Update an existing book |
| DELETE | `/books/delete_book/{title}` | Delete a book by title  |

###### Code: Project 1

```python
# Import FastAPI and Body for building APIs and reading request body
from fastapi import FastAPI, Body

# Create the FastAPI application instance
app = FastAPI()

# In-memory list to store book data (acts like a fake database)
BOOKS = [
    {'title': 'Title One', 'author': 'Author One', 'category': 'science'},
    {'title': 'Title Two', 'author': 'Author Two', 'category': 'science'},
    {'title': 'Title Three', 'author': 'Author Three', 'category': 'history'},
    {'title': 'Title Four', 'author': 'Author Four', 'category': 'math'},
    {'title': 'Title Five', 'author': 'Author Five', 'category': 'math'},
    {'title': 'Title Six', 'author': 'Author One', 'category': 'math'},
]

# Get all books
@app.get("/books")
async def read_all_books():
    return BOOKS


# Get one book by title (Path Parameter)
# Example: /books/Title%20Two
@app.get("/books/{book_title}")
async def read_book(book_title: str):
    for book in BOOKS:
        # Compare titles (case-insensitive)
        if book.get('title').casefold() == book_title.casefold():
            return book


# Get books by category (Query Parameter)
# Example: /books/?category=science
@app.get("/books/")
async def read_book_by_query(category: str):
    books_to_return = []
    for book in BOOKS:
        # Compare categories (case-insensitive)
        if book.get("category").casefold() == category.casefold():
            books_to_return.append(book)

    return books_to_return


# Create a new book (POST + Body)
@app.post("/books/create_book")
async def create_book(new_book = Body()):
    # Add the received book data to the list
    BOOKS.append(new_book)

    # Return the created book
    return new_book


# Update an existing book by title (PUT + Body)
@app.put("/books/update_book")
async def update_book(updated_book = Body()):
    for i in range(len(BOOKS)):
        # Compare titles (case-insensitive)
        if BOOKS[i].get("title").casefold() == updated_book.get("title").casefold():
            # Replace old data with new data
            BOOKS[i] = updated_book

            return updated_book

    # Return message if not found
    return {"message": "Book not found"}


# Delete a book by title (Path Parameter)
# Example: /books/delete_book/Title%20Two
@app.delete("/books/delete_book/{book_title}")
async def delete_book(book_title: str):
    for i in range(len(BOOKS)):
        # Compare titles (case-insensitive)
        if BOOKS[i].get("title").casefold() == book_title.casefold():

            # Remove the matched book
            BOOKS.pop(i)

            # Stop after deleting one
            break

    # Return delete result
    return {"message": "Book deleted (if it existed)"}

```

## Section 6: Project 2 - Move Fast with FastAPI

#### 82. Book 2 Project Overview

Project will be still focusing on creating Book API Endpoints.

This project will include:

- GET, POST, PUT, DELETE Requst Methods
- Data Validation, Error Handling, Status Code, Swagger Configuration, Python Request Objects

###### Creating a New Book Object

A constructor will be created to constructor to initialize the Book object.

```python
# Define a Book class to represent a book object
class Book:

    # Type hints for class attributes
    id: int
    title: str
    author: str
    description: str
    rating: int

    # Initialize a new Book object
    def __init__(self, id, title, author, description, rating):

        # Assign values to object attributes
        self.id = id
        self.title = title
        self.author = author
        self.description = description
        self.rating = rating
```

#### 83. FastAPI Project: Setup Book 2 Project

In this project, we will use `Book` object.

###### Where To Start?

```python
from fastapi import FastAPI

app = FastAPI()

class Book:
    id : int
    title: str
    author: str
    description: str
    rating: int

    def __init__(self, id, title, author, description, rating):
        self.id = id
        self.title = title
        self.author = author
        self.description = description
        self.rating = rating

BOOKS = [
    Book(1, 'Computer Science Pro', 'codingwithroby', 'A very Nice Book!', 5),
    Book(2, 'Be fast with FastAPI', 'codingwithroby', 'A very Nice Book!', 5),
    Book(3, 'Master Endpoints', 'codingwithroby', 'A very Nice Book!', 5),
    Book(4, 'HP1', 'Author 1', 'Book Description', 2),
    Book(5, 'HP2', 'Author 2', 'Book Description', 3),
    Book(6, 'HP3', 'Author 3', 'Book Description', 1),
]


@app.get("/books")
async def read_all_books():
    return BOOKS
```
