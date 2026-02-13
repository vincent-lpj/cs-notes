###### Reference

[FastAPI - The Complete Course 2026 (Beginner + Advanced)](https://www.udemy.com/course/fastapi-the-complete-course/)

## Section 1: Introduction

#### 1. Introduction

This course focuses on learning how to build **RESTful** and **full-stack** applications using **FastAPI**.

It not only teaches how to develop FastAPI applications, but also covers essential knowledge of **full-stack development**.

**No prior FastAPI experience is required** to start this course.

#### 2. Course Content

###### Learning Path / Roadmap

1. Phase 1: Foundations
   - Introduction

   - Python Refresher

2. Phase 2: Backend Projects
   - Project 1 (Restful API endpoint)

   - Project 2 (Class & Error Handling)

   - Project 3 (Database & ORM)

3. Phase 3: Core Features
   - Authentication (JWT)

   - Routing

4. Phase 4: Advanced Backend
   - Project 3.5 (DB & DB Migration)

   - Project 4 (Unit & Integration Testing)

5. Phase 5: Full Stack
   - Project 5 (Full Stack Development)

6. Phase 6: Tooling & Workflow
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

`Abstraction` means hiding the implementation details and showing only the necessary information to the user.

For example, think of a flashlight. It has an "on" and "off" switch. When you turn it on, it produces a beam of light.

You do **NOT** need to know how the light works inside the flashlight; you only need to focus on the switch.

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

Then, in the `main.py` file (similar to using a flashlight):

```python
from Enemy import *

enemy = Enemy();
enemy.talk()  # Here, we only need to focus on calling talk method, instead of caring about what is inside

# I am an enemy!
```

###### Why Use Abstraction?

- This allows users to avoid understanding how the functionality works behind the scenes
- It helps create simple and reusable code
- It encourages better use of the **DRY** principle (Do not repeat yourself)
- It makes Python objects more scalable

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

###### What is Constructor

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

[Official Documentation](https://fastapi.tiangolo.com/)

###### Strength of FastAPI

`FastAPI` is a Python web-framework for building mordern RESTful APIs.

- Few Bugs
- Quick & Easy
- Robust
- Standard

###### Where Does FastAPI Fit with An Application Architecture?

A webpage communicates with a backend server through HTTP APIs (often RESTful).

FastAPI can also render web pages and be used to build full-stack applications.

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

###### Creating a Virtual Environment

We use `pip` and `venv` to create virtual environment for our FastAPI application.

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

###### Installation of FastAPI

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

`async` stands for asynchronous.

- It enables non-blocking execution, allowing the server to handle multiple requests concurrently.

- In traditional synchronous code, each request must finish before the next one starts, which can slow down performance when many users connect at the same time.

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

`uvicorn` is the ASGI web server used to run and serve a FastAPI application.

It：

- handles incoming HTTP requests,
- manages asynchronous communication,
- and connects the FastAPI application to the network.

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

`/docs` is the central page for viewing and testing FastAPI APIs using Swagger UI. It allows you to interact with APIs directly in the browser.

- Show all API endpoints
- Display HTTP methods (GET, POST, etc.)
- Show request parameters
- Display response formats
- Allow online API testing

#### 70. FastAPI Project: Path Parameters Overview

###### What are Path Parameters

`Path parameters` are variables embedded in the URL path that are used to pass data to the server.

- They are usually used to **identify** or **locate** specific resources based on their position in the URL structure

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

`Query parameters` are request parameters (`name=value` pairs) that are attached to the URL after a `?`.

Examples:

URL:

```
127.0.0.1:8000/books/?category=math
```

#### 73. FastAPI Project: Query Parameters

Query parameters are used to **filter**, **sort**, or **paginate** data based on the URL provided. data, based on the url provided.

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

- POST requests can include a **request body**, allowing additional data to be sent

- The request body is usually sent in **JSON format**

  ```json
  { "title": "Title Seven", "author": "Author Two", "category": "math" }
  ```

`Body()` is used to **explicitly declare a request body parameter** in FastAPI.
It tells FastAPI that the data should be read from the **HTTP request body**, not from query parameters or the URL path.

#### 75. FastAPI Project: Post Request

POST is the `Create` method in CRUD operations, so it is used to add new data to the book list.

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
- It usually does not contain a request body

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

It will include:

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

#### 85. FastAPI Project: POST Request Before Valiation

###### Sample Code

`Body()` does not add any validation into our code.

```python
@app.post("/create-book")
async def create_book(book_request = Body()):
    BOOKS.append(book_request)
    return book_request
```

So, we can add books like this, even if it does not make sense. We need to inplement some kind of validation.

```bash
curl -X 'POST' \
  'http://localhost:8000/create-book' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '  {
    "id": -6,
    "title": "HP3",
    "author": "Author 3",
    "description": "Book Description",
    "rating": "low"
  }'
```

#### 86. FastAPI Project: Pydantics and Data Validation Overview

In this section, we will go over [Pydantic](https://docs.pydantic.dev/latest/) .

- A Python library that is used for **data modeling**, **data parsing** and has efficient **error handling**
- Commonly used for data validation in FastAPI

###### How to Use Pydantic in a POST Request

- To validate data, we should separate the Book object from the request data.

- Create a separate request model for data validation: **BookRequest**
  - Inherit from `BaseModel`

  - Use `Field` to define validation rules
  - FastAPI **automatically** validates input data

  ```python
  from pydantic import BaseModel, Field

  class BookRequest(BaseModel):
      id: int
      title: str = Field(min_length=3)
      author: str = Field(min_length=1)
      description: str = Field(min_length=1, max_length=100)
      rating: int = Field(gt=0, lt=6)
  ```

- Convert the Pydantic request model into a `Book` object

  Basic Flow: Validate → Convert → Save

  ```python
  @app.post("/create-book")
  async def create_book(book_request: BookRequest):  # validate
      new_book = Book(**book_request.model_dump())  # convert
      BOOKS.append(new_book)  # save
      return new_book
  ```

#### 87. FastAPI Project: Pydantic Book Request Validation

Here, we add an id checker to make it in a certain sequence.

```python
@app.post("/create-book")
async def create_book(book_request: BookRequest):
    new_book = Book(**book_request.model_dump())
    BOOKS.append(find_book_id(new_book))
    return new_book

def find_book_id(book: Book):
    if len(BOOKS) > 0:
        book.id = BOOKS[-1].id + 1
    else:
        book.id = 1

    return book
```

#### 88. FastAPI Project: Fields - Data Validation

`Field` allow use to add validation to each field of object.

We change the attribute `id` to be optional here, since we have the id checker.

```python
class BookRequest(BaseModel):
    id: Optional[int] = None
    title: str = Field(min_length=3)
    author: str = Field(min_length=1)
    description: str = Field(min_length=1, max_length=100)
    rating: int = Field(gt=0, lt=6)
```

#### 89. FastAPI Project: Pydantic Configuration

`model_config` is used to customize how a Pydantic model **behaves** and **appears** in FastAPI documentation.

- `json_schema_extra` is used to **add extra information to the generated JSON schema**, mainly for documentation purposes.

  It is commonly used to:
  - Provide example request data
  - Improve API readability
  - Help frontend developers understand input format

```python
class BookRequest(BaseModel):
  	# Optional ID (not required when creating a new book)
    id: Optional[int] = Field(description="This id is not needed fo creation", default=None)
    title: str = Field(min_length=3)
    author: str = Field(min_length=1)
    description: str = Field(min_length=1, max_length=100)
    rating: int = Field(gt=0, lt=6)

    # Configure extra schema information for Swagger UI
    # We can check in Swagger UI that example data is displayed
    model_config = {
    "json_schema_extra" : {
        "example": {
            "title": "A new book",
            "author": "codingwithroby",
            "description": "A new description of a book",
            "rating": 5
        }
      }
    }
```

#### 90. FastAPI Project: Fetch Book

Let us create more endpoints.

```python
@app.get('/books/{book_id}')
async def read_book(book_id:int):
    for book in BOOKS:
        if book.id == book_id:
            return book
```

#### 91. FastAPI Project: Fetch Books by Rating

Another endpoint to fetch book by rating:

```python
@app.get("/books/")
async def read_book_by_rating(book_rating: int):
    books_to_return = []
    for book in BOOKS:
        if book.rating == book_rating:
            books_to_return.append(book)
    return books_to_return
```

#### 92. FastAPI Project: Update Book with PUT Request

PUT method allows us to update our data

```python
# Not sure why BookRequest is not converted here
@app.put("/books/update_book")
async def update_book(book: BookRequest):
    for i in range(len(BOOKS)):
        if BOOKS[i].id == book.id:
            BOOKS[i] = book
```

#### 93. FastAPI Project: Delete Book with Delete Request

```python
@app.delete("/books/{book_id}")
async def delete_book(book_id: int):
    for i in range(len(BOOKS)):
        if BOOKS[i].id == book_id:
            BOOKS.pop(i)
            break
```

#### 96. FastAPI Project: Data Validation Path Parameters

In this section, let us continue to add validation to our project.

`Path` allow us to build and validate path parameters.

```python
from fastapi inport Path
@app.get('/books/{book_id}')
async def read_book(book_id:int = Path(gt=0)):
    for book in BOOKS:
        if book.id == book_id:
            return book
```

Now, we not only have validations on our request body and on our path parameters.

#### 97. FastAPI Project: Data Validation Query Parameters

`Query` allow us to add valitation to query parameters.

```python
from fastapi import Query

@app.get("/books/")
async def read_book_by_rating(book_rating: int = Query(gt=0, lt=6)):
    books_to_return = []
    for book in BOOKS:
        if book.rating == book_rating:
            books_to_return.append(book)
    return books_to_return
```

#### 98. FastAPI Project: Status Codes Overview

We will go over `status code`, when dealing with API and API endpoints.

###### Status Code

- An HTTP status code is to help the client (the user or system submitting data to the server) to understand what happened on the server side application
- Status codes are international standards on how **a client/server should handle the result of a request**.
- It allows everyone who sends a request to know it their submission was successful or not.

|     |                      |                                   |
| --- | -------------------- | --------------------------------- |
| 1xx | Information Response | Request processing                |
| 2xx | Success              | Request successfully complete     |
| 3xx | Redirection          | Further action must be complete   |
| 4xx | Client Errors        | An error was caused by the client |
| 5xx | Server Errors        | An error occurred on the server   |

###### 2xx: Successful Status Code

`200: OK`:

- Standard response for a successful request.
- Commonly used for successful **GET** requests when data is being returned

`201: Created`:

- The request has been successful, creating a **new resource**.
- Used when a POST creates an entity

`204: No Content`:

- The request has been successful, did **NOT** create an entity nor return anything.
- Commonly used with **PUT** method

###### 4xx: Client Errors Status Code

`400: Bad Request`:

- Can not process due to client error
- Commonly used for invalid request method

`401: Unauthorized`:

- Client does not have valid authentication for target resource

`404: Not Found`:

- The client requested resource can not be found

`422: Unprocessable Entity`:

- Semantic Errors in client request

###### 5xx: Server Status Code

`500: Internal Server Error`:

- Generic error message, when an unexpected issue on the server happened.
- Such as a failed Python program, etc.

#### 99. FastAPI Project: HTTP Exceptions

Learn how to implement HTTP exceptions.

An `HTTPException` is something we raise within our method, which is to cancel the functionaliy of our method, and return a message and status code to our user.

Use `raise` to raise HTTPException

```python
from fastapi import HTTPException

@app.get('/books/{book_id}')
async def read_book(book_id:int = Path(gt=0)):
    for book in BOOKS:
        if book.id == book_id:
            return book
    raise HTTPException(status_code=404, detail="Item not found")
```

#### 100. FastAPI Project: Explicit Status Code Response

In this section, we will add a **status code response** for a successful API endpoint request.

FastAPI is built on `starlette`, so we can directly import `status` from startlette.

Although FastAPI returns 200 when successful, we can be **explicit** about it.

```python
from starlette import status
```

###### Final Version

```python
from fastapi import FastAPI, Path, Query, HTTPException
from pydantic import BaseModel, Field
from typing import Optional
from starlette import status

app = FastAPI()

class Book:
    id : int
    title: str
    author: str
    description: str
    rating: int
    published_date: int

    def __init__(self, id, title, author, description, rating, published_date):
        self.id = id
        self.title = title
        self.author = author
        self.description = description
        self.rating = rating
        self.published_date = published_date

class BookRequest(BaseModel):
    id: Optional[int] = Field(description="This id is not not needed fo creation", default=None)
    title: str = Field(min_length=3)
    author: str = Field(min_length=1)
    description: str = Field(min_length=1, max_length=100)
    rating: int = Field(gt=0, lt=6)
    published_date: int = Field(gt=1999,lt=2031)

    model_config = {
        "json_schema_extra" : {
            "example": {
                "title": "A new book",
                "author": "codingwithroby",
                "description": "A new description of a book",
                "rating": 5,
                "published_date": 2026
            }
        }
    }

BOOKS = [
    Book(1, 'Computer Science Pro', 'codingwithroby', 'A very Nice Book!', 5, 2030),
    Book(2, 'Be fast with FastAPI', 'codingwithroby', 'A very Nice Book!', 5, 2030),
    Book(3, 'Master Endpoints', 'codingwithroby', 'A very Nice Book!', 5, 2029),
    Book(4, 'HP1', 'Author 1', 'Book Description', 2, 2028),
    Book(5, 'HP2', 'Author 2', 'Book Description', 3, 2027),
    Book(6, 'HP3', 'Author 3', 'Book Description', 1, 2026),
]


@app.get("/books", status_code=status.HTTP_200_OK)
async def read_all_books():
    return BOOKS


@app.get("/books/{book_id}", status_code=status.HTTP_200_OK)
async def read_book(book_id:int = Path(gt=0)):
    for book in BOOKS:
        if book.id == book_id:
            return book
    raise HTTPException(status_code=404, detail="Item not found")

@app.get("/books/", status_code=status.HTTP_200_OK)
async def read_book_by_rating(book_rating: int = Query(gt=0, lt=6)):
    books_to_return = []
    for book in BOOKS:
        if book.rating == book_rating:
            books_to_return.append(book)
    return books_to_return

@app.get("/books/publish/", status_code=status.HTTP_200_OK)
async def read_book_by_publish_date(published_date: int = Query(gt=1999, lt=2031)):
    books_to_return = []
    for book in BOOKS:
        if book.published_date == published_date:
            books_to_return.append(book)
    return books_to_return


@app.post("/create-book", status_code=status.HTTP_201_CREATED)
async def create_book(book_request: BookRequest):
    new_book = Book(**book_request.model_dump())
    BOOKS.append(find_book_id(new_book))
    return new_book

def find_book_id(book: Book):
    book.id = 1 if len(BOOKS) == 0 else BOOKS[-1].id + 1
    return book

# Not sure why BookRequest is not converted here
@app.put("/books/update_book", status_code=status.HTTP_204_NO_CONTENT)
async def update_book(book: BookRequest):
    book_changed = False
    for i in range(len(BOOKS)):
        if BOOKS[i].id == book.id:
            BOOKS[i] = book
            book_changed = True
    if not book_changed:
        raise HTTPException(status_code=404, detail="Item not found")


@app.delete("/books/{book_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_book(book_id: int = Path(gt=0)):
    book_changed = False
    for i in range(len(BOOKS)):
        if BOOKS[i].id == book_id:
            BOOKS.pop(i)
            book_changed = True
            break
    if not book_changed:
        raise HTTPException(status_code=404, detail="Item not found")
```

## Section 7: Project 3: Complete RESTful APIs

#### 101. Project 3: Overview

In project 3, we will be switching our focus to TODOs instead of BOOKS.

New information will include:

- Full SQL Database
  - SQLite
  - (later) PostgreSQL, MySQL
- Authentication
  - JWT
- Authorization
- Hashing Passwords
  - Hashing algorithm

###### Outline of Project 3

```
       Authorization              Retrieving the user
       Authentication              and saving Todos
  Web       ---------->    FastAPI     ---------->     Database
  Page      <---------      Server     <---------
```

## Section 8: Setup Database

#### 103. FastAPI Project: SQL Database Introduction

###### What is a Database?

- Organized collection of structured information of data, which is stored in a computer system.
  - Organized in how data can be retrieved, stored, and modified
  - A database allows management of data
  - Database Management Systems (DBMS) like SQLite, MySQL, and PostgreSQL
- The data can be
  - easily accessed
  - modified
  - Controlled and organized
- Many databases use a structured query lanaguage (SQL) to modify and write data

###### What is a SQL?

- Standard language for dealing with relational databases.
  - Create
  - Read
  - Update
  - Delete

#### 104. FastAPI Project: Database Connection with ORM SQLAlchemy

```
pip install sqlalchemy
```

`database.py`

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base
# from sqlalchemy.ext.declarative import declarative_base  # Old import (SQLAlchemy v1)


# Database connection URL (connects to a local SQLite file)
SQLALCHEMY_DATABASE_URL = "sqlite:///./todos.db"


# Create database engine (responsible for connecting to the database)
# SQLite requires check_same_thread=False for FastAPI (multi-thread support)
engine = create_engine(
    SQLALCHEMY_DATABASE_URL,
    connect_args={"check_same_thread": False}
)


# Create a database session factory
# SessionLocal is used to create database sessions
# Sessions are used to query, insert, update, and delete data
SessionLocal = sessionmaker(
    autocommit=False,   # Do not save changes automatically
    autoflush=False,    # Do not send changes to DB automatically
    bind=engine         # Bind sessions to this engine
)


# Base class for all ORM models
# All database models must inherit from this class
# Used to collect table metadata for table creation
Base = declarative_base()
```

#### 105. FastAPI Project: Database Tables (Models)

`models.py`

**Models** is a way for SQL alchemy to be able to understand what kind of database tables we are going to be creating within our database in the future.

###### Table Structure: Todos

| id (PK) | title | description | priority | Complete |
| ------- | ----- | ----------- | -------- | -------- |
|         |       |             |          |          |

###### ORM Mapping

```python
from database import Base
from sqlalchemy import Column, Integer, String, Boolean

# Define a database model for the "todos" table (ORM model)
# This class maps a Python object to a database table
# One object = one row, one class = one table
class Todos(Base):
    __tablename__ = "todos"  # Specify the table name in the database

    id = Column(Integer, primary_key=True, index=True)   # Primary key column (unique ID for each todo)
    title = Column(String)
    description = Column(String)
    priority = Column(Integer)
    complete = Column(Boolean, default=False)            # Stored as 0/1 in the database
```

#### 106. FastAPI Project: Main (Crate Database Connection for API)

`main.py`

```python
from fastapi import FastAPI
import models
from database import engine


# Create FastAPI application
app = FastAPI()


# Create database tables from ORM models
# Base → collects all table models
# metadata → stores table structure
# create_all → creates missing tables
# bind=engine → connects to the database
models.Base.metadata.create_all(bind=engine)

```

SQLAchedemy will create database and table inside when we first open this FastAPI application.

```bash
uvicorn main:app --reload
```

###### Conception of Database Creation

```python
                ┌───────────────┐
                │   Database    │
                │ (SQLite/MySQL)│
                └───────▲───────┘
                        │
                        │  (connect)
                    ┌───┴───┐
                    │ Engine│
                    └───▲───┘
                        │
                        │  (bind)
              ┌─────────┴─────────┐
              │    SessionLocal    │
              │ (Session Factory)  │
              └─────────▲─────────┘
                        │
                        │  create
                    ┌───┴───┐
                    │Session│
                    └───▲───┘
                        │
                        │  use
        ┌───────────────┴───────────────┐
        │           ORM Models          │
        │   (Todos, Users, Tasks, ...)  │
        └───────────────▲───────────────┘
                        │
                        │  inherit
                    ┌───┴───┐
                    │  Base │
                    └───────┘

```

#### 108. FastAPI Project: Installation of SQLite3 Terminal (Mac)

[SQLite Home Page](https://sqlite.org/)

SQLite is shipped with [Home Brew](https://sqlite.org/)

```python
brew list
```

Then, we can enter SQLite using the following command:

```python
sqlite3
# SQLite version 3.43.2 20**-**-** **:**:**
# Enter ".help" for usage hints.
# Connected to a transient in-memory database.
# Use ".open FILENAME" to reopen on a persistent database.
# sqlite>
```

#### 109. FastAPI Project: SQL Queries Introduction

###### Inserting Database Tables

```sqlite
INSERT INTO todos (title, description, priority, complete) VALUES ("Go to store", "To pick up eggs", 4, false);
```

Then, we can insert more data:

```sqlite
INSERT INTO todos (title, description, priority, complete) VALUES ("Haircut", "Need to get length 1mm", 3, false);
INSERT INTO todos (title, description, priority, complete) VALUES ("Feed dog", "Make sure to use new food brand", 5, false);
```

###### Select SQL Queries

```sqlite
-- Select ALL columns and rows
SELECT * FROM todos;

-- Select just title from columns
SELECT title FROM todos;

-- Select title, description from columns
SELECT title, description FROM todos;
```

###### WHERE Clause

`WHERE clause` specifies the cretieria that a field values must meet for the records that contains the values be included in the query results.

```sqlite
-- Select ALL rows & columns WHERE priority=5
SELECT * FROM todos WHERE priority=5;

SELECT * FROM todos WHERE title="Feed dog";

SELECT * FROM todos WHERE id=2;
```

###### UPDATE Clause

`UPDATE clause` is used when we want to update a record in the database.

```sqlite
-- Update ALL rows & columns to now have complete=True WHERE id=5
UPDATE todos SET complete=True WHERE id=5;

UPDATE todos SET complete=True WHERE title="Learn something new";
```

###### DELETE Clause

`DELETE clause` is to delete a record from a database.

```sqlite
-- Delete ALL rows & columns where id = 5
DELETE FROM todos WHERE id=5;

DELETE FROM todos WHERE complete=0;
```

#### 110. FastAPI Project: SQLite3 Setting up Todos

In this lecture, we will manipulate SQLite3 database using our terminal.

```bash
sqlite3 todos.db

# Get help infos
.help

# Show all tables in our current database
.schema

# Get a nicer look of the table
.mode column
# .mode markdown
# .mode box
# .mode table
```

## Section 9: API Request Methods

#### 111. FastAPI Project: Get All Todos from Database

Note: `Base.metadata.create_all(bind=engine)` will not enhance our DB if it already exists. We will learn more about enhancing it in **Alembic Section of Course**.

###### Depends and Annotated in FastAPI

Core Concepts

- Depends → Injects values

- Annotated → Adds metadata

`Depends`

- **Purpose**: Handles Dependency Injection (DI).
- **Mechanism**: Tells FastAPI to execute a function/callable _before_ the route logic.
- **Chainable**: A dependency can depend on another dependency (creating a dependency tree).

`Annotated`

- **Standard Python**: Introduced in Python 3.9 (`typing.Annotated`).
- **The Mix**: `Annotated[Type, Metadata]`
- **FastAPI Usage**: `Annotated[DataType, Depends(logic_function)]`

Example:

```python
# --- Dependency Declaration ---

# Parameter type:   Session (The object used in the function)
# Parameter source: get_db() (The logic that provides the object)
# Annotated:        Merges the 'Type' with the 'Dependency Logic'
DB_Session = Annotated[Session, Depends(get_db)]
# --- Behind the Scenes (How FastAPI handles it) ---

# When an endpoint uses 'db: DB_Session', FastAPI will:
# 1. Resolve: Execution triggers the 'get_db' callable.
# 2. Extract: Capture the yielded/returned value from 'get_db'.
# 3. Inject:  Assign that value to the 'db' variable before entering the route.
```

###### main.py

Dependency Injecttion

Let FastAPI automatically provide required objects (like DB sessions) to your functions.

```python
from typing import Annotated
from fastapi import FastAPI, Depends
from sqlalchemy.orm import Session
import models
from models import Todos
from database import engine, SessionLocal


# Create FastAPI application
app = FastAPI()


# Create database tables from ORM models (if they do not exist)
# Base → collects all models
# metadata → stores table info
# create_all → creates missing tables
# bind=engine → connects to DB
models.Base.metadata.create_all(bind=engine)


# Database dependency function
# Provides a database session for each request
def get_db():
    # 1. SETUP: Code before 'yield' runs BEFORE the request starts.
    db = SessionLocal()
    try:
        yield db  # 2. INJECT: This value is passed to the endpoint.
    finally:
        # 3. TEARDOWN: Code after 'yield' runs AFTER the response is sent.
        # This happens even if the endpoint raised an error.
        db.close()


# Create a reusable database dependency type
# Session → expected type
# Depends(get_db) → get session from get_db()
db_dependency = Annotated[Session, Depends(get_db)]


# Get all todos from the database
# db: Session = Depends(get_db)
# is the same as
# db: Annotated[Session, Depends(get_db)]
@app.get("/", status_code=status.HTTP_200_OK)
async def read_all(db: db_dependency):

    # Query all records from the Todos table
    return db.query(Todos).all()
```

###### Try It out!

```bash
curl -X 'GET' \
  'http://localhost:8000/read_all' \
  -H 'accept: application/json'
```

#### 112. FastAPI Project: Get Todo by ID

```python
@app.get("/todo/{todo_id}", status_code=status.HTTP_200_OK)
async def read_todo(
    db: db_dependency,                 # Inject database session
    todo_id: int = Path(gt=0)           # Path parameter (must be > 0)
):

    # Query the Todos table and find the record by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).first()

    # If the todo exists, return it
    if todo_model is not None:
        return todo_model

    # If not found, return 404 error
    raise HTTPException(
        status_code=404,
        detail="Todo not found."
    )
```

#### 113. FastAPI Project: POST Request (Todo Project)

```python
# Request model for creating a new Todo
# ID is not included because SQLite will generate it automatically
class TodoRequst(BaseModel):
    title: str = Field(min_length=3)
    description: str = Field(min_length=3, max_length=100)
    priority: int = Field(gt=0, lt=6)
    complete: bool

@app.post("/todo", status_code=status.HTTP_201_CREATED)
async def create_todo(db: db_dependency, todo_request: TodoRequst):
    # Convert Pydantic model to ORM model
    todo_model = Todos(**todo_request.model_dump())

    # Add the new record to the session
    db.add(todo_model)

    # Save changes to the database
    db.commit()
```

#### 114. FastAPI Project: Put Request (Todo Project)

###### ORM Upadate Rule

To update data, first query the ORM object, then modify the fields of the **same ORM object** and commit.
Do not create a new object to replace it.

```python
@app.put("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def update_todo(db: db_dependency,todo_request: TodoRequst, todo_id: int = Path(gt=0)):
    # Find the todo item by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).first()

    # If not found, return 404 error
    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found.")

    # Update fields using request data
    todo_model.title = todo_request.title
    todo_model.description = todo_request.description
    todo_model.priority = todo_request.priority
    todo_model.complete = todo_request.complete

    db.add(todo_model)    # Add updated object to session
    db.commit()						# Save changes to the database
```

###### Try It out!

```bash
curl -X 'PUT' \
  'http://localhost:8000/todo/3' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '  {
    "complete": true,
    "description": "Make sure to use new food brand",
    "priority": 1,
    "title": "Feed dog"
  }'
```

#### 115. FastAPI Project: Delete Request (Todo Project)

```python
@app.delete("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_todo(db: db_dependency, todo_id: int = Path(gt=0)):
    todo_model = db.query(Todos).filter(Todos.id == todo_id).first()
    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found")
    db.query(Todos).filter(Todos.id == todo_id).delete()
    db.commit()
```

```bash
curl -X 'DELETE' \
  'http://localhost:8000/todo/5' \
  -H 'accept: */*'
```

#### Todo Project – Self Review Notes

###### Project Structure

- main.py (API entry)

- models.py (ORM models)

- database.py (DB config)

###### ORM Workflow

```
query()   → Find data
add()     → Insert
commit()  → Save
refresh() → Reload
delete()  → Remove
close()   → Cleanup
```

###### API Endpoint

| Action   | Method | Endpoint   |
| -------- | ------ | ---------- |
| Read All | GET    | /          |
| Read     | GET    | /todo/{id} |
| Create   | POST   | /todo      |
| Update   | PUT    | /todo/{id} |
| Delete   | DELETE | /todo/{id} |

###### Source Code

`main.py`

```python
from typing import Annotated

from pydantic import BaseModel, Field
from sqlalchemy.orm import Session
from fastapi import FastAPI, Depends, HTTPException, Path
from starlette import status

import models
from models import Todos
from database import engine, SessionLocal


# Create FastAPI application
app = FastAPI()


# Create database tables from ORM models (if they do not exist)
# Base → collects all models
# metadata → stores table info
# create_all → creates missing tables
# bind=engine → connects to DB
models.Base.metadata.create_all(bind=engine)


# Database dependency function
# Provides a database session for each request
def get_db():
    # Create a new database session
    db = SessionLocal()

    try:
        yield db        # Give the session to FastAPI
    finally:
        db.close()      # Always close the session after request ends


# Create a reusable database dependency type
# Session → expected type
# Depends(get_db) → get session from get_db()
db_dependency = Annotated[Session, Depends(get_db)]

# Request model for creating a new Todo
# ID is not included because SQLite will generate it automatically
class TodoRequst(BaseModel):
    title: str = Field(min_length=3)
    description: str = Field(min_length=3, max_length=100)
    priority: int = Field(gt=0, lt=6)
    complete: bool


# Get all todos from the database
@app.get("/", status_code=status.HTTP_200_OK)
async def read_all(db: db_dependency):
    # Query all records from the Todos table
    return db.query(Todos).all()


# Inject database session: db_dependency
# Path parameter (must be > 0): Path(gt=0)
@app.get("/todo/{todo_id}", status_code=status.HTTP_200_OK)
async def read_todo(db: db_dependency, todo_id: int = Path(gt=0)):
    # Query the Todos table and find the record by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).first()

    # If the todo exists, return it
    if todo_model is not None:
        return todo_model

    # If not found, return 404 error
    raise HTTPException(status_code=404, detail="Todo not found.")

@app.post("/todo", status_code=status.HTTP_201_CREATED)
async def create_todo(db: db_dependency, todo_request: TodoRequst):
    # Convert Pydantic model to ORM model
    todo_model = Todos(**todo_request.model_dump())

    db.add(todo_model)          # Add the new record to the session
    db.commit()                 # Save changes to the database


@app.put("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def update_todo(db: db_dependency,todo_request: TodoRequst, todo_id: int = Path(gt=0)):
    # Find the todo item by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).first()

    # If not found, return 404 error
    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found.")

    # Update fields on the existing ORM object
    # This allows SQLAlchemy to track changes and perform an UPDATE
    todo_model.title = todo_request.title
    todo_model.description = todo_request.description
    todo_model.priority = todo_request.priority
    todo_model.complete = todo_request.complete

    db.add(todo_model)              # Add updated object to session
    db.commit()						# Save changes to the database

@app.delete("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_todo(db: db_dependency, todo_id: int = Path(gt=0)):
    todo_model = db.query(Todos).filter(Todos.id == todo_id).first()
    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found")
    db.delete(todo_model)           # Delete the record
    db.commit()                     # Save changes to the database
```

`database.py`

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base
# from sqlalchemy.ext.declarative import declarative_base  # Old import (SQLAlchemy v1)


# Database connection URL (connects to a local SQLite file)
SQLALCHEMY_DATABASE_URL = "sqlite:///./todos.db"


# Create database engine (responsible for connecting to the database)
# SQLite requires check_same_thread=False for FastAPI (multi-thread support)
engine = create_engine(
    SQLALCHEMY_DATABASE_URL,
    connect_args={"check_same_thread": False}
)


# Create a database session factory
# SessionLocal is used to create database sessions
# Sessions are used to query, insert, update, and delete data
SessionLocal = sessionmaker(
    autocommit=False,   # Do not save changes automatically
    autoflush=False,    # Do not send changes to DB automatically
    bind=engine         # Bind sessions to this engine
)


# Base class for all ORM models
# All database models must inherit from this class
# Used to collect table metadata for table creation
Base = declarative_base()
```

`models.py`

```python
from database import Base
from sqlalchemy import Column, Integer, String, Boolean

# Define a database model for the "todos" table (ORM model)
# This class maps a Python object to a database table
# One object = one row, one class = one table
class Todos(Base):
    __tablename__ = "todos"  # Specify the table name in the database

    id = Column(Integer, primary_key=True, index=True)   # Primary key column (unique ID for each todo)
    title = Column(String)
    description = Column(String)
    priority = Column(Integer)
    complete = Column(Boolean, default=False)            # Stored as 0/1 in the database
```

## Section 10: Authentication & Authorization

#### 116. FastAPI Project: Starting Authentication & Authorization

In this section, we start working on authentication and authorization for our application.

As our application is growing, how do we **scale** our application for cleaness and maintenability is very important.

So, we will create a new file, `auth.py` in our root folder.

#### 117. FastAPI Project: Routers Scale Authentication File

###### Router

Routers help separate API endpoints into different files.

The main file acts as the entry point, and each router manages its own routes, which improves code organization and readability.

- Create a `routers` folder to separate route logic from main application code.

- Move `auth.py` into `routers` to improve project maintainability.

- In `auth.py`:

  ```python
  from fastapi import APIRouter

  # Create a router instance for grouping related endpoints
  router = APIRouter()

  # Authentication-related endpoint
  # This route will be registered in main.py using include_router()
  @router.get("/auth/")
  async def get_user():

      # Return authentication status (example response)
      return {"user": "authenticated"}
  ```

- In `main.py`:

  ```python
  from routers import auth

  # Register authentication-related routes
  app.include_router(auth.router)
  ```

#### 118. FastAPI Project: Router Scale Todos File

In this section, we keep cleaning up our application for scalability and maintenability.

- Create a `todos.py` in `routes` folder
- Move todos related endpoints from `main.py` to `todos.py`

###### Current Project File Structure (With Routes)

```
todo_project/
│
├── main.py                # Application entry point (create app, register routers)
│
├── database.py            # Database config (engine, SessionLocal, Base)
│
├── models.py              # ORM models (Todos table)
│
├── routers/               # Route modules (API endpoints)
│   │
│   ├── __init__.py        # Makes routers a Python package
│   ├── auth.py            # Authentication-related routes
│   └── todos.py           # Todo CRUD routes
│
├── requirements.txt       # Project dependencies
│
└── todos.db               # SQLite database file
```

#### 119. FastAPI Project: One to Many Relationships

###### What is A One Two Many Relationships

- A user can have many todos
- We use `owner` as **foreign key** in todos table to connect it to users table

###### todos

| id(PK) | title | description | priority | complete | owner(FK) |
| ------ | ----- | ----------- | -------- | -------- | --------- |
|        |       |             |          |          |           |

###### users

| id(PK) | email | username | first_name | last_name | hased_password | is_active |
| ------ | ----- | -------- | ---------- | --------- | -------------- | --------- |
|        |       |          |            |           |                |           |

- Each API request, a user will have their ID attached
  - If we have the user ID attached to each request, we can use the ID to find their todos.

#### 120. FastAPI Project: Foreign Keys

###### What is A Foreign Key?

A `foreign key` is a column within a relational database table that provides a **link** between two separate tables.

- A foreign key references a primary key of another table

#### 121. FastAPI Project: Users Table Creation

1. Firstly, we change our DB's name: `todos` -> `todosapp`
   - In `database.py`, we

     ```python
     # Database connection URL (connects to a local SQLite file)
     SQLALCHEMY_DATABASE_URL = "sqlite:///./todosapp.db"
     ```

   - This will create a database called "todosapp" after we start the app

2. Then, we create `users` table
   - In `models.py`, we

     ```python
     # ORM model for the "users" table (one class = one table)
     class Users(Base):
         __tablename__ = "users"                              # Table name in database

         id = Column(Integer, primary_key=True, index=True)    # Unique user ID (primary key)
         email = Column(String, unique=True)                   # User email (must be unique)
         username = Column(String, unique=True)                # Username (must be unique)
         first_name = Column(String)                           # User first name
         last_name = Column(String)                            # User last name
         hashed_password = Column(String)                      # Encrypted password (never store plain text)
         is_active = Column(Boolean, default=True)             # Account status (active / disabled)
         role = Column(String)                                 # User role (e.g., admin, user)
     ```

   - This will add a new table called `users` after we start the app

3. Finally, we add a column of `owner_id` in `todos` table

   ```python
   owner_id = Column(Integer, ForeignKey("users.id"))    # Link to users.id (foreign key)
   ```

#### 122. FastAPI Project: Create First User

In this section, we start to enhance our `auth.py`

```python
from fastapi import APIRouter
from pydantic import BaseModel
from models import Users


# Create a router instance for grouping authentication-related endpoints
router = APIRouter()


# Request model for creating a new user
# Used to validate incoming JSON data
class CreateUserRequest(BaseModel):
    user_name: str
    email: str
    first_name: str
    last_name: str
    password: str
    role: str


# Create user endpoint (example for learning purpose)
# This route will be registered in main.py using include_router()
@router.post("/auth")
async def create_user(create_user_request: CreateUserRequest):

    # Convert Pydantic request model into ORM model
    # Note: We cannot directly use **model_dump()
    # because the password must be processed (hashed) first
    # This part will be improved later
    create_user_model = Users(
        email=create_user_request.email,
        username=create_user_request.user_name,
        first_name=create_user_request.first_name,
        last_name=create_user_request.last_name,
        role=create_user_request.role,

        # Temporary: store raw password (for learning only)
        # In real projects, always hash passwords before saving
        hashed_password=create_user_request.password,

        is_active=True
    )

    # Temporary: return ORM object without saving to database
    # Database session and commit will be added later
    return create_user_model

```

#### 123. FastAPI Project: Hash User's Password

Because we do not want to save passwords directly in our database, we need to **hash** users' passwords.

1. `passlib` and `bcrypt` are used in our application.

   ```bash
   pip install passlib
   pip install bcypt==4.0.1
   ```

2. Create a password hashing context using bcrypt algorithm
   - **bcrypt_context** will be used to hash and verify passwords

   ```python
   from passlib.context import CryptContext
   bcrypt_context = CryptContext(schemes=['bcrypt'], depreciated='auto')
   ```

3. Hash the user's plain text password before storing it
   - In `User`:

   ```python
   hashed_password = bcrypt_context.hash(create_user_request.password),
   ```

#### 124. FastAPI Project: Save User to Database

1. Import `Depends`, `Session`, `Annotated`, `status`

   ```
   from fastapi import APIRouter, Depends
   from sqlalchemy.orm import Session
   from typing import Annotated
   from starlette import status
   ```

2. Import `SessionLocal`

   ```
   from database import SessionLocal
   ```

3. Write dependency injection

   ```
   @router.post("/auth", status_code=status.HTTP_201_CREATED)
   async def create_user(db: db_dependency,
                         create_user_request: CreateUserRequest):
   ```

4. Add and commit to db

   ```python
   db.add(create_user_model)
   db.commit()
   ```

#### 125. FastAPI Project: Authenticate A User

Authentication and authorization is introduced in the following serveral videos.

Here, we create a new endpoint, `/token`, which return a token (JWT) including all information about a user.

###### Login Authentication – Step-by-Step Notes

1. Install multipart support
   - Without this package, OAuth2 login will not work.

     ```bash
     pip install python-multipart
     ```

2. Import OAuth2 login form
   - FastAPI uses this class to extract login credentials.

   - Provides a standard login form structure

     ```python
     from fastapi.security import OAuth2PasswordRequestForm
     ```

3. Create user authentication function

   ```python
   # Verify user credentials (username + password)
   def authenticate_user(username: str, password: str, db):

       # Find user by username in the database
       user = db.query(Users).filter(Users.username == username).first()

       # If user does not exist, authentication fails
       if not user:
           return False

       # Verify the input password against the stored hashed password
       if not bcrypt_context.verify(password, user.hashed_password):
           return False

       return True				# Authentication successful
   ```

4. Implement login endpoint
   - Receive form → Authenticate → Return result

     ```python
     # Login endpoint for generating access tokens (authentication)
     @router.post("/token")
     async def login_for_access_token(
         form_data: Annotated[OAuth2PasswordRequestForm, Depends()],  # Get login form data
         db: db_dependency                                           # Inject database session
     ):

         # Check if username and password are valid
         user = authenticate_user(form_data.username, form_data.password, db)

         # If authentication fails, return error message
         if not user:
             return "Failed Authentication"

         # If authentication succeeds, return success message
         # (Token generation will be added later)
         return "Successful Authentication"
     ```

5. Test login in Swagger UI
   - Login form appears with: username and password

#### 126. JSON Web Token (JWT) Overview

###### What is a JSON Web Token?

`JSON Web Token`is a self-contained way to securely transmit data and information between two parties using a **JSON Object**.

- It can be trusted because each JWT can be digitally assigned, so server can know if the JWT has been changed or not.
- JWT should be used in **authorization**, not **authentication**
- Test and learn more about JWT at [JSON Web Tokens](https://www.jwt.io/)

###### JSON Web Token Structure

A JWT is created of three separate parts, each of them separated with dot (.)

```
aaaaaaa.bbbbbb.cccccc
```

- Header (a)

  The JWT header is encoded using Base64
  - alg: The algorithm of signing
  - typ: the specific type of token

- Payload (b)

  A JWT payload consists of the **data**, and encoded using Base64

- Signature (c)

  A JWT signature is created using the algorithm in the header to hash out the encoded header, encoded payload with a secret.
  - The **secret** is saved on the server so that the client does not have access to it.

###### JWT Example

1. JWT Header

   ```json
   {
     "alg": "HS256",
     "typ": "JWT"
   }
   ```

2. JWT Payload

   ```json
   {
     "sub": "123456789",
     "name": "Eric Roby",
     "given_name": "Eric",
     "family_name": "Roby",
     "email": "codingwithroby@email.com",
     "admin": true
   }
   ```

3. JWT

   ```
   HMACSHA256(
   	base64UrlEncode(header) + "." +
   	base64UrlEncode(payload),
   	learnonline)
   ```

#### 127. FastAPI Project: Encode A JSON Web Token (JWT)

1. Install necessary library

   ```bash
   pip install "python-jose[cryptography]"
   ```

2. Generate your secret key
   - Generate your secret key using `openssl`

     ```bash
     openssl rand -hex 32
     ```

   - Write your secret key and algorithm in your application

     ```python
     SECRET_KEY = 'xxx'
     ```

3. Write encoder function

   ```python
   from datetime import timedelta, datetime, timezone
   from jose import jwt

   def create_access_token(username: str, user_id: str, expires_delta: timedelta):
       # Create JWT payload (user identity information)
       encode = {
           "sub": username,   # Subject (usually the username)
           "id": user_id      # User ID
       }

       # Calculate token expiration time (UTC)
       expired = datetime.now(timezone.utc) + expires_delta

       # Add expiration time to payload
       encode.update({"exp": expired})

       # Encode and sign the JWT using secret key and algorithm
       return jwt.encode(encode, SECRET_KEY, algorithm=ALGORITHM)
   ```

4. Complet the
   - Set response model

     ```python
     class Token(BaseModel):
         access_token: str
         token_type: str
     ```

   - Login → Verify → Generate Token → Return Token

     ```python
     # Login endpoint that returns a JWT access token
     @router.post("/token", response_model=Token)
     async def login_for_access_token(form_data: Annotated[OAuth2PasswordRequestForm, Depends()], db: db_dependency):
         # Authenticate user using username and password
         user = authenticate_user(form_data.username, form_data.password, db)

         # If authentication fails, return 401
         if not user:
             raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail="Invalid username or password")

         # Generate JWT access token (valid for 20 minutes)
         token = create_access_token(user.username, user.id, timedelta(minutes=20))

         # Return token in standard OAuth2 format
         return {"access_token": token, "token_type": "bearer"}
     ```

#### 128. FastAPI Project: Decode a JSON Web Token (JWT)

```python
oauth2_bearer = OAuth2PasswordBearer(tokenUrl='token')
```

```python
from fastapi.security import OAuth2PasswordBearer
from jose import jwt, JWTError


# Dependency function to get the currently logged-in user
# It verifies the JWT and extracts user information
async def get_current_user(
    token: Annotated[str, Depends(oauth2_bearer)]  # Get token from Authorization header
):

    try:
        # Decode and verify the JWT using secret key and algorithm
        payload = jwt.decode(token, SECRET_KEY, ALGORITHM)

        # Extract user information from token payload
        username: str = payload.get("sub")   # Subject (username)
        user_id: int = payload.get("id")     # User ID

        # If required fields are missing, authentication fails
        if username is None or user_id is None:
            raise HTTPException(
                status_code=status.HTTP_401_UNAUTHORIZED,
                detail="Could not validate user."
            )

        # Return user info (can be used in protected endpoints)
        return {
            "username": username,
            "id": user_id
        }


    # If token is invalid, expired, or tampered with
    except JWTError:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Could not validate user."
        )

```

#### 129. FastAPI Project: Authentication Enhancement

To seperate auth-related endpoints,

```python
# Create a router for authentication-related endpoints
# prefix → adds "/auth" to all routes in this module
# tags   → groups these routes under "auth" in Swagger UI
router = APIRouter(
    prefix="/auth",
    tags=["auth"]
)
```

#### Auth – Self Review Notes

The authentication system is built using OAuth2 password flow with JWT-based authorization, bcrypt password hashing, and FastAPI dependency injection for secure and scalable user authentication.

| Category             | Technology / Library   | Purpose                  | Description                                                      |
| -------------------- | ---------------------- | ------------------------ | ---------------------------------------------------------------- |
| Framework            | FastAPI                | API Framework            | Handles routing, dependency injection, and request processing    |
| Protocol             | OAuth2 (Password Flow) | Authentication Standard  | Provides standardized login workflow using username and password |
| Token System         | JWT (JSON Web Token)   | Stateless Authentication | Stores user identity in signed tokens for authorization          |
| Security             | Passlib + Bcrypt       | Password Hashing         | Encrypts passwords before storing in the database                |
| Cryptography         | Python-JOSE            | JWT Encryption           | Encodes and decodes JWT tokens with digital signatures           |
| Dependency Injection | Depends / Annotated    | Dependency Management    | Injects database sessions and authentication logic               |
| Token Transport      | Bearer Token           | Authorization Header     | Sends JWT via `Authorization: Bearer <token>`                    |
| Validation           | Pydantic               | Data Validation          | Validates login and registration requests                        |
| ORM                  | SQLAlchemy             | User Data Access         | Queries and manages user records                                 |
| API Docs             | Swagger (OpenAPI)      | API Testing              | Provides interactive login and token testing interface           |

###### Source Code

`auth.py`

```python
from datetime import timedelta, datetime, timezone
from typing import Annotated
from fastapi import APIRouter, Depends, HTTPException
from pydantic import BaseModel
from sqlalchemy.orm import Session
from starlette import status
from database import SessionLocal
from models import Users
from passlib.context import CryptContext
from fastapi.security import OAuth2PasswordRequestForm, OAuth2PasswordBearer
from jose import jwt, JWTError

# Create a router instance for grouping related endpoints
router = APIRouter(
    prefix="/auth",
    tags=['auth']
)

SECRET_KEY = 'xxx'
ALGORITHM = 'HS256'

# Create a password hashing context using bcrypt algorithm
# This is used to securely hash and verify passwords
bcrypt_context = CryptContext(schemes=['bcrypt'], deprecated='auto')

oauth2_bearer = OAuth2PasswordBearer(tokenUrl='auth/token')


class CreateUserRequest(BaseModel):
    user_name: str
    email: str
    first_name: str
    last_name: str
    password: str
    role: str

class Token(BaseModel):
    access_token: str
    token_type: str



def get_db():
    db = SessionLocal()

    try:
        yield db        # Give the session to FastAPI
    finally:
        db.close()      # Always close the session after request ends


# Create a reusable database dependency type
db_dependency = Annotated[Session, Depends(get_db)]

def authenticate_user(username:str, password:str, db):
    user = db.query(Users).filter(Users.username == username).first()
    if not user:
        return False
    if not bcrypt_context.verify(password, user.hashed_password):
        return False
    return user

def create_access_token(username: str, user_id: str, expires_delta: timedelta):
    # Create JWT payload (user identity information)
    encode = {
        "sub": username,   # Subject (usually the username)
        "id": user_id      # User ID
    }

    # Calculate token expiration time (UTC)
    expired = datetime.now(timezone.utc) + expires_delta

    # Add expiration time to payload
    encode.update({"exp": expired})

    # Encode and sign the JWT using secret key and algorithm
    return jwt.encode(encode, SECRET_KEY, algorithm=ALGORITHM)

# Dependency function to get the currently logged-in user
# It verifies the JWT and extracts user information
async def get_current_user(
    token: Annotated[str, Depends(oauth2_bearer)]  # Get token from Authorization header
):

    try:
        # Decode and verify the JWT using secret key and algorithm
        payload = jwt.decode(token, SECRET_KEY, ALGORITHM)

        # Extract user information from token payload
        username: str = payload.get("sub")   # Subject (username)
        user_id: int = payload.get("id")     # User ID

        # If required fields are missing, authentication fails
        if username is None or user_id is None:
            raise HTTPException(
                status_code=status.HTTP_401_UNAUTHORIZED,
                detail="Could not validate user."
            )

        # Return user info (can be used in protected endpoints)
        return {
            "username": username,
            "id": user_id
        }


    # If token is invalid, expired, or tampered with
    except JWTError:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Could not validate user."
        )



# Authentication-related endpoint
# This route will be registered in main.py using include_router()
@router.post("/", status_code=status.HTTP_201_CREATED)
async def create_user(db: db_dependency,
                      create_user_request: CreateUserRequest):
    # We can not use **CreateUserRequest.model_dump()
    # Because the password and hashed_password do not match
    # and need further processing
    create_user_model = Users(
        email = create_user_request.email,
        username = create_user_request.user_name,
        first_name = create_user_request.first_name,
        last_name = create_user_request.last_name,
        role = create_user_request.role,
        hashed_password = bcrypt_context.hash(create_user_request.password),
        is_active = True
    )

    db.add(create_user_model)
    db.commit()


# Login endpoint that returns a JWT access token
@router.post("/token", response_model=Token)
async def login_for_access_token(form_data: Annotated[OAuth2PasswordRequestForm, Depends()], db: db_dependency):
    # Authenticate user using username and password
    user = authenticate_user(form_data.username, form_data.password, db)

    # If authentication fails, return 401
    if not user:
        raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail="Invalid username or password")

    # Generate JWT access token (valid for 20 minutes)
    token = create_access_token(user.username, user.id, timedelta(minutes=20))

    # Return token in standard OAuth2 format
    return {"access_token": token, "token_type": "bearer"}
```

## Section 11. Authenticate Requests

#### 130. FastAPI Project: POST Todo (User ID)

1. Define Authentication Dependency

   Use `Depends(get_current_user)` to extract and validate the JWT token from the request header.
   - This dependency will return the current user info after decoding the token.

   - All protected routes should use this dependency.

     ```python
     from .auth import get_current_user
     user_dependency = Annotated[dict, Depends(get_current_user)]
     ```

2. Verify User and Bind Data to User

   Inject `user` into the route so FastAPI automatically checks the token.
   - First, verify that `user` is not `None` to block unauthenticated access.

   - When creating data, use `user['id']` as `owner_id` to link records to the logged-in user.

     ```python
     @router.post("/todo", status_code=status.HTTP_201_CREATED)
     async def create_todo(user: user_dependency, db: db_dependency, todo_request: TodoRequst):
         if user is None:
             raise HTTPException(status_code=401, detail='Authentication Failed')

         # Convert Pydantic model to ORM model
         # Remember to add foreign key
         todo_model = Todos(**todo_request.model_dump(), owner_id = user.get('id'))

         db.add(todo_model)          # Add the new record to the session
         db.commit()                 # Save changes to the database
     ```

3. Send Request with Bearer Token
   - The client must include a valid JWT token in the `Authorization` header using the `Bearer` format.

   - The backend uses this token to identify the user. Missing or invalid tokens will result in a 401 error.

     ```bash
     curl -X 'POST' \
       'http://localhost:8000/todo' \
       -H 'accept: application/json' \
       -H 'Authorization: Bearer aaa.bbb.ccc' \
       -H 'Content-Type: application/json' \
       -d '{
       "title": "Learn FastAPI",
       "description": "Because it is awesome",
       "priority": 5,
       "complete": false
     }'
     ```

#### 131. FastAPI Project: Get All Todos (User ID)

###### Get All Todos of Specific User

Instead of fetching all todos in the database, this endpoint only returns the todos that belong to the currently authenticated user.

This ensures:

- Users can only access their own data
- Data privacy and security are enforced
- The API follows access control rules

```python
# Get all todos that belong to the current user
# The user information is extracted from the JWT token
@router.get("/", status_code=status.HTTP_200_OK)
async def read_all(user: user_dependency, db: db_dependency):
    if user is None:
      raise HTTPException(status_code=401, detail='Authentication Failed')

    # Query todos where owner_id matches the current user's ID
    return db.query(Todos).filter(Todos.owner_id == user.get("id")).all()
```

#### 132. FastAPI Project: GET Todo (ID + User ID)

Here, a simple filter `.filter(Todos.owner_id == user.get('id'))` will do the trick

```python
# Inject database session: db_dependency
# Path parameter (must be > 0): Path(gt=0)
@router.get("/todo/{todo_id}", status_code=status.HTTP_200_OK)
async def read_todo(user: user_dependency, db: db_dependency, todo_id: int = Path(gt=0)):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication Failed')

    # Query the Todos table and find the record by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).filter(Todos.owner_id == user.get('id')).first()

    # If the todo exists, return it
    if todo_model is not None:
        return todo_model

    # If not found, return 404 error
    raise HTTPException(status_code=404, detail="Todo not found.")
```

#### 133. FastAPI Project: PUT Todo (User ID)

Same as above, we identify user by `user_dependency` and filter it by `filter(Todos.owner_id) == user.get('id')`

```python
@router.put("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def update_todo(user: user_dependency, db: db_dependency,todo_request: TodoRequst, todo_id: int = Path(gt=0)):
    if user is None:
        return HTTPException(status_code=401, detail='Authentication Failed')

    # Find the todo item by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).filter(Todos.owner_id == user.get('id')).first()

    # If not found, return 404 error
    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found.")

    # Update fields on the existing ORM object
    # This allows SQLAlchemy to track changes and perform an UPDATE
    todo_model.title = todo_request.title
    todo_model.description = todo_request.description
    todo_model.priority = todo_request.priority
    todo_model.complete = todo_request.complete

    db.add(todo_model)              # Add updated object to session
    db.commit()						# Save changes to the database
```

#### 134. FastAPI Project: Delete Todo (User ID)

The logic is totally same as above.

```python
@router.delete("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_todo(user: user_dependency, db: db_dependency, todo_id: int = Path(gt=0)):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication Failed')

    todo_model = db.query(Todos).filter(Todos.id == todo_id).filter(Todos.owner_id == user.get('id')).first()

    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found")

    db.delete(todo_model)           # Delete the record
    db.commit()                     # Save changes to the database
```

#### 135. FastAPI Project: Admin Router

In this section, we are going to create a router called `admin`, where only user with role of `admin` can have access to its endpoints.

1. Create `admin.py` in `router` folder:
   - This file should have `router`,
   - This file should import `get_current_user` from `auth`, and `SessionLocal` from `database`
   - This file should have `db_dependency` and `user_dependency`

2. Add `role` key/value pairs in jwt encoding (in `auth.py`)
   - Add role in `create_access_token`, in the `encode` dictionary

     ```python
     def create_access_token(username: str, user_id: str, role: str, expires_delta: timedelta):
         # Create JWT payload (user identity information)
         encode = {
             "sub": username,   # Subject (usually the username)
             "id": user_id,      # User ID
             "role": role
         }

         # Calculate token expiration time (UTC)
         expired = datetime.now(timezone.utc) + expires_delta

         # Add expiration time to payload
         encode.update({"exp": expired})

         # Encode and sign the JWT using secret key and algorithm
         return jwt.encode(encode, SECRET_KEY, algorithm=ALGORITHM)
     ```

   - Add role in `get_user_role`, returnning `user_role`

     ```python
     # Dependency function to get the currently logged-in user
     # It verifies the JWT and extracts user information
     async def get_current_user(
         token: Annotated[str, Depends(oauth2_bearer)]  # Get token from Authorization header
     ):

         try:
             # Decode and verify the JWT using secret key and algorithm
             payload = jwt.decode(token, SECRET_KEY, ALGORITHM)

             # Extract user information from token payload
             username: str = payload.get("sub")   # Subject (username)
             user_id: int = payload.get("id")     # User ID
             user_role: str = payload.get("role")

             # If required fields are missing, authentication fails
             if username is None or user_id is None:
                 raise HTTPException(
                     status_code=status.HTTP_401_UNAUTHORIZED,
                     detail="Could not validate user."
                 )

             # Return user info (can be used in protected endpoints)
             return {
                 "username": username,
                 "id": user_id,
                 "user_role": user_role
             }
     ```

3. Add endpoints for `admin`
   - If the newly added `user_role` is not admin, this request will not be executed.

   ```python
   @router.get("/todo", status_code=status.HTTP_200_OK)
   async def read_all(user: user_dependency, db: db_dependency):
       if user is None or user.get("user_role") != "admin":
           raise HTTPException(status_code=401, detail="Authentication Failed")
       return db.query(Todos).all()
   ```

4. Add routers in `main.py`

   ```
   app.include_router(admin.router)    # Register admin-related routes
   ```

#### 137. FastAPI Project: Assignment Solution (User Route)

1. Create `users.py` in `route` folder

2. Set up router in this file

   ```python
   router = APIRouter(
       prefix="/user",
       tags=['user']
   )
   ```

3. Get ready of the following variables
   - `db_dependency`
   - `user_dependency`
   - `bcrypt_context`

4. Add routers in `main.py`

   ```
   app.include_router(users.router)
   ```

5. Create `/` endpoint of `get_users`

   ```python
   @router.get("/", status_code=status.HTTP_200_OK)
   async def get_user(user: user_dependency, db: db_dependency):
       if user is None:
           raise HTTPException(status_code=401, detail='Authentication failed')
       user_model = db.query(Users).filter(Users.id == user.get("id")).first()
       if user_model is None:
           raise HTTPException(status_code=404, detail='User not found')
       return user_model
   ```

6. Create `/password` endpoint to change a user's password
   - Create a Pydantic class of `UserVerification`

     ```python
     class UserVerfification(BaseModel):
         password: str
         new_password: str = Field(min_length=6)
     ```

   - Create a `PUT` method

     ```python
     @router.put("/password", status_code=status.HTTP_204_NO_CONTENT)
     async def change_password(user: user_dependency, db: db_dependency, user_verification : UserVerfification):
         if user is None:
             raise HTTPException(status_code=401, detail='Authentication failed')
         user_model = db.query(Users).filter(Users.id == user.get('id')).first()
         if not bcrypt_context.verify(user_verification.password, user_model.hashed_password):
             raise HTTPException(status_code=401, detail='Error on password')
         user_model.hashed_password = bcrypt_context.hash(user_verification.new_password)
         db.add(user_model)
         db.commit()
     ```

## Section 12: Large Production Database Setup

#### 138. FastAPI Project: Production DBMS

In this section, we will

1. Install the production DBMS

2. Setup the table and data within the production DBMS

3. Connect the production DBMS to our application

4. Push data from application to our production DBMS

###### Production Database

This section we will go over installing a **production relational database** for your application.

- MySQL

- PostgreSQL

###### Difference between SQLite and Production DBMS

SQLite:

- Runs in-memery or local-disk
- Can be deployed along with your application
- Emphasize economy, efficiency, and simplicity

Production DBMS

- Runs on their own server and port
- Needed to be deployed separately from your application
- Focus on sealability, concurrency, and control

#### 139. PostgreSQL Introduction

###### What is PostgreSQL

PostgreSQL is extremely popular and production-ready.

It is an **open-source** relational database management system.

It requires a server to be run.

###### Who Use/Used PostgreSQL

Apple, Reddit and Twitch

#### 141. FastAPI Project: PostgreSQL Mac Installation

[Official Website of PostgreSQL](https://www.postgresql.org/)

###### Installation of Postgres.app

1. Download PostgreSQL from [Download](https://postgresapp.com/downloads.html)

2. Install Postgres.app

3. Initialize Postgres

4. In the [Installation Page](https://postgresapp.com/), copy and run the following command in terminal

   ```bash
   sudo mkdir -p /etc/paths.d &&
   echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp
   ```

5. Install [pgAdmin](https://www.postgresql.org/download/) to our system

#### 142. FastAPI Project: PostegreSQL Create Database Table

In this section, we are going to create a production database.

1. In PgAdmin, register a server
   1. Make sure Postgres.app is running
   2. Servers -> register
   3. Set the server
      - General -> Name -> `TodoApplicationServer`
      - Connection -> Host name/address -> `localhost`
      - Password -> `yourpassword`
      - Click `save`

2. Check the server created
   - The server created will host `databases` and `users`
   - Make sure that there is a supersuer called `postgres`
     - Right click user `postgres` -> `Privileges` -> make sure `superuser` is checked

3. Create database
   - There are two databases already exists
     - Database named `your-user-name`
     - Database named `postgres`
   - We are going create `TodoApplicationDatabase`
     - Right click `Databases`
     - Create -> Database ->
       - General: Database `TodoApplicationDatabase`
       - Definition -> Template -> `template0`
       - Click Save

4. Create tables
   - Tables are shown in Databases -> TodoAppDatabase -> `schema` -> `Tables`

   - We are going to create tables with `Query Tools` at the top bar.

     ```sql
     DROP TABLE IF EXISTS users;

     CREATE TABLE users (
       id SERIAL,
       email varchar(200) DEFAULT NULL,
       username varchar(45) DEFAULT NULL,
       first_name varchar(45) DEFAULT NULL,
       last_name varchar(45) DEFAULT NULL,
       hashed_password varchar(200) DEFAULT NULL,
       is_active boolean DEFAULT NULL,
       role varchar(45) DEFAULT NULL,
       PRIMARY KEY (id)
     );

     DROP TABLE IF EXISTS todos;

     CREATE TABLE todos (
       id SERIAL,
       title varchar(200) DEFAULT NULL,
       description varchar(200) DEFAULT NULL,
       priority integer  DEFAULT NULL,
       complete boolean  DEFAULT NULL,
       owner_id integer  DEFAULT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (owner_id) REFERENCES users(id)
     );
     ```

   - Then, we will have our two new tables, `users` and `todos`

     ```
     NOTICE:  table "users" does not exist, skipping
     NOTICE:  table "todos" does not exist, sipping
     CREATE TABLE

     Query returned successfully in 31 msec.
     ```

#### 143. FastAPI Project: PostgreSQL Connect to FastAPI

Let's connect our FastAPI application to this database.

1. Install necessary library

   ```bash
   pip install psycopg2-binary-2.9.6
   ```

2. Change database connection url:

   ```python
   # Database connection URL (connects to a local SQLite file)
   # SQLALCHEMY_DATABASE_URL = "sqlite:///./todosapp.db"

   # Database connection URL for PostgreSQL
   # Format: postgresql://<username>:<password>@<host>/<database_name>
   # This connects the application to the local PostgreSQL database
   SQLALCHEMY_DATABASE_URL = "postgresql://xxx:your-password@localhost/TodoApplicationDatabase"
   ```

3. Adjust the engine configuration

   ```python
   # Create database engine (responsible for connecting to the database)
   # SQLite requires check_same_thread=False for FastAPI (multi-thread support)
   # engine = create_engine(
   #     SQLALCHEMY_DATABASE_URL,
   #     connect_args={"check_same_thread": False}
   # )

   # PostgreSQL (or other production databases) engine configuration
   # No special thread configuration is required
   engine = create_engine(SQLALCHEMY_DATABASE_URL)
   ```

4. Then, postgres is ready for usage

   ```bash
   uvicorn main:app --reload
   ```

#### 144. MySQL Introduction

###### What is MySQL

- Open-source relational database management system
- Require a server
- Production ready
- Scalable
- Secure

###### Who Uses/Used MySQL

Facebook/YouTube/Tesla

#### 146. FastAPI Project: MySQL Installation (Mac)

###### Download MySQL

[Official Website](https://www.mysql.com/)

1. Find MySQL downloads
   - MySQL Download -> MySQL Community Server
   - Download ARM, DMG Archive
2. Installing MySQL
   - Install for all users
   - Set passwords for `root` user
3. Check MySQL in our system
   - Click Apple sign -> `System Preference`
   - MySQL is at the bottom

Because the following section will use PostgreSQL, the rest part of MySQL tutorial is skipped

## Section 13: Project 3.5 Alembic Data Migration

#### 149. Alembic Data Migration Overview

###### What is Alembic

`Alembic` is a **light-weight** data migration tool when using SQLAlchemy

- Allow us to plan, transfer, and upgrade resources within databases
- Allow us to **change** a SQLAlchemy database **table** after it has been created
- Allow us to modify the database schemes

###### How does Alembic Work

1. We already have some data within our database
2. Alembic helps us to create a new column on the table that already exists
3. For example: a `phone-number` column for `users` table

#### 150. Alembic Introduction

1. Installing **Alembic** into our project

   ```bash
   pip install alembic
   ```

2. Alembic commands

   ```bash
   alembic init <folder name>
   alembic revision -m <message>
   alembic update <revision #>
   alembic downgrade -1
   ```

3. When using Alembic, two new items will appear in our directory
   - alembic.ini
   - alembic directory
     - versions
     - env.py
     - README
     - script.py.mako

#### 151. Alembic Installation and Setup

In this section, alembic is added to modify the databases without deleting it.

（following the instructions above)

#### 152. Alembic Revisions Overview

###### Alembic Revision

`Alembic Revision` is how we can create a new alembic file where we can add some type of database upgrade.

It:

- Create a new file where we can write the upgrade code
- Each revision will have a Revision Id

```bash
alembic revision -m "create phone number col on users table"
```

###### Alembic Upgrade

`Alembic Upgrade` is how we actually run the migration.

The following code will enhance our database to now have a new column within our user tables called `phone_number`

```python
def upgrade() -> None:
	op.add_column('users', sa.Column('phone_number', sa.String(), nullable=True))
```

To run the alembic upgrade:

```bash
alembic upgrade <revision id>
```

###### Alembic Downgrade

`Alembic Downgrade` is how we revert a migration.

```python
def downgrade() -> None:
	op.drop_column('users', 'phone_number')
```

To run the alembic downgrade:

```bash
alembic downgrade -1
```

#### 153. Alembic Revision Upgrade

In this video, we configure **Alembic database migrations** for our project and apply a schema change step by step.

1. Modify the `users` model in `models.py`
   - First, we update the ORM model by adding a new column to the `users` table.

     ```python
     phone_number = Column(String)
     ```

   - This change only updates the Python model and **does not affect the database yet**.

2. Configure the database URL in `alembic.ini`
   - Next, we set the database connection string in `alembic.ini`. You can refer to `database.py` to ensure the URL is consistent.

     ```ini
     # sqlalchemy.url = driver://user:pass@localhost/dbname
     sqlalchemy.url = postgresql://xxx:your-password@localhost/TodoApplicationDatabase
     ```

   - This allows Alembic to connect to the correct PostgreSQL database.

3. Update `env.py` in the `alembic` directory
   - To enable Alembic’s **autogenerate** feature, we must link Alembic to our SQLAlchemy models.

     ```python
     import models

     # this is the Alembic Config object, which provides
     # access to the values within the .ini file in use.
     config = context.config

     # Interpret the config file for Python logging.
     # This line sets up loggers basically.
     # if config.config_file_name is not None:
     #     fileConfig(config.config_file_name)
     fileConfig(config.config_file_name)

     # add your model's MetaData object here
     # for 'autogenerate' support
     # from myapp import mymodel
     # target_metadata = mymodel.Base.metadata
     # ↓ target_metadata = None
     target_metadata = models.Base.metadata
     ```

   - By setting `target_metadata`, Alembic can compare the current database schema with our ORM models.

4. Create a new Alembic revision
   - Now we generate a migration file to record the schema change.

     ```bash
     alembic revision -m "create phone number for user column"
     ```

   - After running this command, a new `.py` file will be created in the `alembic/versions` directory.

   - Example migration file:

     ```python
     def upgrade() -> None:
         """Upgrade schema."""
         op.add_column('users', sa.Column('phone_number', sa.String(), nullable = True))
     ```

   - At this stage, **the database is still unchanged**—we have only created a migration script.

5. Apply the migration to the database
   - Finally, we run the upgrade command to apply the schema change.

     ```bash
     alembic upgrade <version #>
     ```

   - After the upgrade completes successfully, you should see output similar to:

     ```bash
     # INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
     # INFO  [alembic.runtime.migration] Will assume transactional DDL.
     # INFO  [alembic.runtime.migration] Running upgrade  -> xxx, create phone number for user column
     ```

   - This confirms that the database schema has been updated.

#### 154. Alembic Revision Downgrade

In the same migration file, we can set the `downgrade` function:

```python
def downgrade() -> None:
    """Downgrade schema."""
    op.drop_column('users', 'phone_number')
```

If we would like to reverse what we have done, run the command below:

```bash
alembic downgrade -1
```

#### 155. Alembic Assignment

1. Add a `phone number` field as required when we create a new user within our `auth.py` file

2. Create a new `@put` request in our `users.py` file that allows a user to update their `phone_number`

#### 156. Alembic Solution

###### Assignment 1

1. Modify `CreateUserRequest`

   ```python
   class CreateUserRequest(BaseModel):
       user_name: str
       email: str
       first_name: str
       last_name: str
       password: str
       role: str
       phone_number: str
   ```

2. Modify `create_user_model` in `create_user` endpoint accordingly

###### Assignment 2

1. Add a new endpoint `change_phone_number` in `users.py`

   ```python
   @router.put("/phonenumber/{phone_number}", status_code=status.HTTP_204_NO_CONTENT)
   async def change_phone_number(user:user_dependency, db:db_dependency, phone_number: str):
       if user is None:
           raise HTTPException(status_code=401, detail='Authentication Failed')
       user_model = db.query(Users).filter(Users.id == user.get('id')).first()
       user_model.phone_number = phone_number
       db.add(user_model)
       db.commit()
   ```

## Project Review: Todo

#### Project Directory Structure

```
todoapp/
│
├── alembic/                 # Database migration system
│   ├── versions/            # Migration scripts (version history)
│   ├── env.py               # Alembic runtime configuration
│   ├── README               # Alembic documentation
│   └── script.py.mako       # Migration template
│
├── routers/                 # API routing layer
│   ├── __init__.py
│   ├── admin.py             # Admin endpoints
│   ├── auth.py              # Authentication endpoints
│   ├── todos.py             # Todo management endpoints
│   └── users.py             # User management endpoints
│
├── test/                    # Test cases
│   └── *.py
│
├── __init__.py
├── alembic.ini              # Alembic global config
├── database.py              # Database connection & session
├── main.py                  # Application entry point
└── models.py                # ORM models
```

#### Overall Layered Architecture

This project follows a typical **FastAPI + SQLAlchemy + Alembic** layered design.

```
┌────────────────────┐
│    API Layer       │   → routers/
│ (Request Handling) │
└────────────────────┘
           ↓
┌────────────────────┐
│   Model Layer      │   → models.py
│ (ORM Mapping)      │
└────────────────────┘
           ↓
┌────────────────────┐
│ Database Layer     │   → database.py + alembic/
│ (Persistence)      │
└────────────────────┘

```

#### Runtime Request Flow

Example: Client sends request to create a todo.

```
Client
   ↓
main.py (FastAPI App)
   ↓
routers/todos.py
   ↓
models.py (ORM)
   ↓
database.py (Session)
   ↓
Database
```

#### Source Code

###### Application Entry (main.py)

Main responsibilities:

- Create FastAPI instance
- Register routers
- Start server

```python
from fastapi import FastAPI
import models
from database import engine
from routers import auth, todos, admin, users

# Create the FastAPI application instance
# This is the entry point of the entire project
app = FastAPI()

# Create database tables based on ORM models
# If the tables already exist, this will do nothing
models.Base.metadata.create_all(bind=engine)

app.include_router(auth.router)     # Register authentication-related routes
app.include_router(todos.router)    # Register todo-related routes
app.include_router(admin.router)    # Register admin-related routes
app.include_router(users.router)
```

###### API Layer (routers/)

Main responsibilities:

- Receive HTTP requests
- Validate parameters
- Call database/business logic
- Return responses

| File     | Responsibility       |
| -------- | -------------------- |
| auth.py  | Authentication / JWT |
| users.py | User management      |
| todos.py | Todo CRUD            |
| admin.py | Admin features       |

`auth.py`

```python
from datetime import timedelta, datetime, timezone
from typing import Annotated
from fastapi import APIRouter, Depends, HTTPException
from pydantic import BaseModel
from sqlalchemy.orm import Session
from starlette import status
from database import SessionLocal
from models import Users
from passlib.context import CryptContext
from fastapi.security import OAuth2PasswordRequestForm, OAuth2PasswordBearer
from jose import jwt, JWTError

# Create a router instance for grouping related endpoints
router = APIRouter(
    prefix="/auth",
    tags=['auth']
)

SECRET_KEY = os.getenv("SECRET_KEY")
ALGORITHM = 'HS256'

# Create a password hashing context using bcrypt algorithm
# This is used to securely hash and verify passwords
bcrypt_context = CryptContext(schemes=['bcrypt'], deprecated='auto')

oauth2_bearer = OAuth2PasswordBearer(tokenUrl='auth/token')


class CreateUserRequest(BaseModel):
    user_name: str
    email: str
    first_name: str
    last_name: str
    password: str
    role: str
    phone_number: str

class Token(BaseModel):
    access_token: str
    token_type: str


def get_db():
    db = SessionLocal()

    try:
        yield db        # Give the session to FastAPI
    finally:
        db.close()      # Always close the session after request ends


# Create a reusable database dependency type
db_dependency = Annotated[Session, Depends(get_db)]

def authenticate_user(username:str, password:str, db):
    user = db.query(Users).filter(Users.username == username).first()
    if not user:
        return False
    if not bcrypt_context.verify(password, user.hashed_password):
        return False
    return user

def create_access_token(username: str, user_id: str, role: str, expires_delta: timedelta):
    # Create JWT payload (user identity information)
    encode = {
        "sub": username,   # Subject (usually the username)
        "id": user_id,      # User ID
        "role": role
    }

    # Calculate token expiration time (UTC)
    expired = datetime.now(timezone.utc) + expires_delta

    # Add expiration time to payload
    encode.update({"exp": expired})

    # Encode and sign the JWT using secret key and algorithm
    return jwt.encode(encode, SECRET_KEY, algorithm=ALGORITHM)

# Dependency function to get the currently logged-in user
# It verifies the JWT and extracts user information
async def get_current_user(
    token: Annotated[str, Depends(oauth2_bearer)]  # Get token from Authorization header
):

    try:
        # Decode and verify the JWT using secret key and algorithm
        payload = jwt.decode(token, SECRET_KEY, ALGORITHM)

        # Extract user information from token payload
        username: str = payload.get("sub")   # Subject (username)
        user_id: int = payload.get("id")     # User ID
        user_role: str = payload.get("role")

        # If required fields are missing, authentication fails
        if username is None or user_id is None:
            raise HTTPException(
                status_code=status.HTTP_401_UNAUTHORIZED,
                detail="Could not validate user."
            )

        # Return user info (can be used in protected endpoints)
        return {
            "username": username,
            "id": user_id,
            "user_role": user_role
        }


    # If token is invalid, expired, or tampered with
    except JWTError:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Could not validate user."
        )



# Authentication-related endpoint
# This route will be registered in main.py using include_router()
@router.post("/", status_code=status.HTTP_201_CREATED)
async def create_user(db: db_dependency,
                      create_user_request: CreateUserRequest):
    # We can not use **CreateUserRequest.model_dump()
    # Because the password and hashed_password do not match
    # and need further processing
    create_user_model = Users(
        email = create_user_request.email,
        username = create_user_request.user_name,
        first_name = create_user_request.first_name,
        last_name = create_user_request.last_name,
        role = create_user_request.role,
        hashed_password = bcrypt_context.hash(create_user_request.password),
        is_active = True,
        phone_number = create_user_request.phone_number
    )

    db.add(create_user_model)
    db.commit()


# Login endpoint that returns a JWT access token
@router.post("/token", response_model=Token)
async def login_for_access_token(form_data: Annotated[OAuth2PasswordRequestForm, Depends()], db: db_dependency):
    # Authenticate user using username and password
    user = authenticate_user(form_data.username, form_data.password, db)

    # If authentication fails, return 401
    if not user:
        raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail="Invalid username or password")

    # Generate JWT access token (valid for 20 minutes)
    token = create_access_token(user.username, user.id, user.role, timedelta(minutes=20))

    # Return token in standard OAuth2 format
    return {"access_token": token, "token_type": "bearer"}
```

`users.py`

```python
from typing import Annotated
from fastapi import APIRouter, Depends, HTTPException, Path
from pydantic import BaseModel, Field
from sqlalchemy.orm import Session
from starlette import status
from database import SessionLocal
from models import Users
from passlib.context import CryptContext


from .auth import get_current_user

# Create a router instance for grouping related endpoints
router = APIRouter(
    prefix="/user",
    tags=['user']
)

def get_db():
    db = SessionLocal()

    try:
        yield db        # Give the session to FastAPI
    finally:
        db.close()      # Always close the session after request ends


class UserVerfification(BaseModel):
    password: str
    new_password: str = Field(min_length=6)

# Create a reusable database dependency type
db_dependency = Annotated[Session, Depends(get_db)]
user_dependency = Annotated[dict, Depends(get_current_user)]
# Create a password hashing context using bcrypt algorithm
# This is used to securely hash and verify passwords
bcrypt_context = CryptContext(schemes=['bcrypt'], deprecated='auto')


@router.get("/", status_code=status.HTTP_200_OK)
async def get_user(user: user_dependency, db: db_dependency):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication failed')
    user_model = db.query(Users).filter(Users.id == user.get("id")).first()
    if user_model is None:
        raise HTTPException(status_code=404, detail='User not found')
    return user_model

@router.put("/password", status_code=status.HTTP_204_NO_CONTENT)
async def change_password(user: user_dependency, db: db_dependency, user_verification : UserVerfification):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication failed')
    user_model = db.query(Users).filter(Users.id == user.get('id')).first()
    if not bcrypt_context.verify(user_verification.password, user_model.hashed_password):
        raise HTTPException(status_code=401, detail='Error on password')
    user_model.hashed_password = bcrypt_context.hash(user_verification.new_password)
    db.add(user_model)
    db.commit()

# Maybe using request body is better?
@router.put("/phonenumber/{phone_number}", status_code=status.HTTP_204_NO_CONTENT)
async def change_phone_number(user:user_dependency, db:db_dependency, phone_number: str):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication Failed')
    user_model = db.query(Users).filter(Users.id == user.get('id')).first()
    user_model.phone_number = phone_number
    db.add(user_model)
    db.commit()
```

`todos.py`

```python
from typing import Annotated

from pydantic import BaseModel, Field
from sqlalchemy.orm import Session
from fastapi import Depends, HTTPException, Path, APIRouter
from starlette import status

from models import Todos
from database import SessionLocal

from .auth import get_current_user

# Create a router instance for grouping related endpoints
router = APIRouter()


# Database dependency function
# Provides a database session for each request
def get_db():
    # Create a new database session
    db = SessionLocal()

    try:
        yield db        # Give the session to FastAPI
    finally:
        db.close()      # Always close the session after request ends


# Create a reusable database dependency type
# Session → expected type
# Depends(get_db) → get session from get_db()
db_dependency = Annotated[Session, Depends(get_db)]

user_dependency = Annotated[dict, Depends(get_current_user)]

# Request model for creating a new Todo
# ID is not included because SQLite will generate it automatically
class TodoRequst(BaseModel):
    title: str = Field(min_length=3)
    description: str = Field(min_length=3, max_length=100)
    priority: int = Field(gt=0, lt=6)
    complete: bool


# Get all todos that belong to the current user
# The user information is extracted from the JWT token
@router.get("/", status_code=status.HTTP_200_OK)
async def read_all(user: user_dependency, db: db_dependency):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication Failed')
    # Query todos where owner_id matches the current user's ID
    return db.query(Todos).filter(Todos.owner_id == user.get('id')).all()


# Inject database session: db_dependency
# Path parameter (must be > 0): Path(gt=0)
@router.get("/todo/{todo_id}", status_code=status.HTTP_200_OK)
async def read_todo(user: user_dependency, db: db_dependency, todo_id: int = Path(gt=0)):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication Failed')

    # Query the Todos table and find the record by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).filter(Todos.owner_id == user.get('id')).first()

    # If the todo exists, return it
    if todo_model is not None:
        return todo_model

    # If not found, return 404 error
    raise HTTPException(status_code=404, detail="Todo not found.")


@router.post("/todo", status_code=status.HTTP_201_CREATED)
async def create_todo(user: user_dependency, db: db_dependency, todo_request: TodoRequst):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication Failed')

    # Convert Pydantic model to ORM model
    # Remember to add foreign key
    todo_model = Todos(**todo_request.model_dump(), owner_id = user.get('id'))

    db.add(todo_model)          # Add the new record to the session
    db.commit()                 # Save changes to the database


@router.put("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def update_todo(user: user_dependency, db: db_dependency,todo_request: TodoRequst, todo_id: int = Path(gt=0)):
    if user is None:
        return HTTPException(status_code=401, detail='Authentication Failed')

    # Find the todo item by ID
    todo_model = db.query(Todos).filter(Todos.id == todo_id).filter(Todos.owner_id == user.get('id')).first()

    # If not found, return 404 error
    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found.")

    # Update fields on the existing ORM object
    # This allows SQLAlchemy to track changes and perform an UPDATE
    todo_model.title = todo_request.title
    todo_model.description = todo_request.description
    todo_model.priority = todo_request.priority
    todo_model.complete = todo_request.complete

    db.add(todo_model)              # Add updated object to session
    db.commit()						# Save changes to the database

@router.delete("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_todo(user: user_dependency, db: db_dependency, todo_id: int = Path(gt=0)):
    if user is None:
        raise HTTPException(status_code=401, detail='Authentication Failed')

    todo_model = db.query(Todos).filter(Todos.id == todo_id).filter(Todos.owner_id == user.get('id')).first()

    if todo_model is None:
        raise HTTPException(status_code=404, detail="Todo not found")

    db.delete(todo_model)           # Delete the record
    db.commit()                     # Save changes to the database


```

`admin.py`

```python
from typing import Annotated

from pydantic import BaseModel, Field
from sqlalchemy.orm import Session
from fastapi import Depends, HTTPException, Path, APIRouter
from starlette import status

from models import Todos
from database import SessionLocal

from .auth import get_current_user

# Create a router instance for grouping related endpoints
router = APIRouter(
    prefix='/admin',
    tags=['admin']
)


# Database dependency function
# Provides a database session for each request
def get_db():
    # Create a new database session
    db = SessionLocal()

    try:
        yield db        # Give the session to FastAPI
    finally:
        db.close()      # Always close the session after request ends


# Create a reusable database dependency type
# Session → expected type
# Depends(get_db) → get session from get_db()
db_dependency = Annotated[Session, Depends(get_db)]
user_dependency = Annotated[dict, Depends(get_current_user)]

@router.get("/todo", status_code=status.HTTP_200_OK)
async def read_all(user: user_dependency, db: db_dependency):
    if user is None or user.get("user_role") != "admin":
        raise HTTPException(status_code=401, detail="Authentication Failed")
    return db.query(Todos).all()

@router.delete("/todo/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_todo(user:user_dependency, db: db_dependency, todo_id: int = Path(gt=0)):
    if user is None or user.get('user_role') != "admin":
        raise HTTPException(status_code=401, detail='Authentication Failed')
    todo_model = db.query(Todos).filter(Todos.id == todo_id).first()
    if todo_model is None:
        raise HTTPException(status_code=404, detail='Todo not found')
    db.delete(todo_model)
    db.commit()
```

###### Database Layer (database.py)

Main responsibilities:

- Create engine
- Manage sessions
- Handle connections

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base
# from sqlalchemy.ext.declarative import declarative_base  # Old import (SQLAlchemy v1)


# Database connection URL (connects to a local SQLite file)
# SQLALCHEMY_DATABASE_URL = "sqlite:///./todosapp.db"

# Database connection URL for PostgreSQL
# Format: postgresql://<username>:<password>@<host>/<database_name>
# This connects the application to the local PostgreSQL database
SQLALCHEMY_DATABASE_URL = "postgresql://xxx:xxxx@localhost/TodoApplicationDatabase"

# Create database engine (responsible for connecting to the database)
# SQLite requires check_same_thread=False for FastAPI (multi-thread support)
# engine = create_engine(
#     SQLALCHEMY_DATABASE_URL,
#     connect_args={"check_same_thread": False}
# )

# PostgreSQL (or other production databases) engine configuration
# No special thread configuration is required
engine = create_engine(SQLALCHEMY_DATABASE_URL)


# Create a database session factory
# SessionLocal is used to create database sessions
# Sessions are used to query, insert, update, and delete data
SessionLocal = sessionmaker(
    autocommit=False,   # Do not save changes automatically
    autoflush=False,    # Do not send changes to DB automatically
    bind=engine         # Bind sessions to this engine
)


# Base class for all ORM models
# All database models must inherit from this class
# Used to collect table metadata for table creation
Base = declarative_base()
```

###### Model Layer (models.py)

Defines ORM mappings between Python objects and database tables.

Main responsibilities:

- Define table structure
- Maintain relationships
- Provide ORM abstraction

```python
from database import Base
from sqlalchemy import Column, ForeignKey, Integer, String, Boolean


# ORM model for the "users" table (one class = one table)
class Users(Base):
    __tablename__ = "users"                              # Table name in database

    id = Column(Integer, primary_key=True, index=True)    # Unique user ID (primary key)
    email = Column(String, unique=True)                   # User email (must be unique)
    username = Column(String, unique=True)                # Username (must be unique)
    first_name = Column(String)                           # User first name
    last_name = Column(String)                            # User last name
    hashed_password = Column(String)                      # Encrypted password (never store plain text)
    is_active = Column(Boolean, default=True)             # Account status (active / disabled)
    role = Column(String)                                 # User role (e.g., admin, user)
    phone_number = Column(String)


# ORM model for the "todos" table (one class = one table)
class Todos(Base):
    __tablename__ = "todos"                               # Table name in database

    id = Column(Integer, primary_key=True, index=True)    # Unique todo ID (primary key)
    title = Column(String)                                # Todo title
    description = Column(String)                          # Todo description
    priority = Column(Integer)                            # Priority level (1 = low, 5 = high)
    complete = Column(Boolean, default=False)             # Completion status (0 = False, 1 = True)
    owner_id = Column(Integer, ForeignKey("users.id"))    # Link to users.id (foreign key)
```

###### Migration Layer (alembic/)

| Component      | Purpose               |
| -------------- | --------------------- |
| versions/      | History of migrations |
| env.py         | Migration runtime     |
| script.py.mako | Template              |

###### Test Layer (test/)

Responsibilities:

- Unit tests
- API tests
- Regression tests

## Section 14: Project 4 - Unit & Integration Test

#### 157. Testing Overview

This section includes `unit testing` and `intergration testing`

###### What is Testing

`Testting` is a way for us to make sure our application is working as intended

It is

- Part of Software Development Lifecycle (SDLC) that identify bugs, errors, and defects
- Make sure user requirements and specfication

Includes:

- Manual Testing
- Unit Testing
- Intergration Testing

###### Unit Testing

It involves testing `individual components` or `units` of software in isolation from the rest of the application.

- **Unit** is testable part of the application
- Tests are automated and executed by a `testing framework` (Pytest)
- Unit testing helps to identify bugs early in development process

###### Integration Testing

It focuses on testing the `interaction` between different units or components.

- The scope is broader than unit testing
- It helps to identify problems for the entire solution
- Examples like calling an API endpoint and make sure the correct solution is returned.

###### Pytest

Pytest is a popular testing framework for Python.

- Simple & Flexible
- Fixtures
- Parameterized Testing

#### 158. Getting Started with Testing Overview

A typical pytest flow includes the following steps:

1. Install `Pytest`

   ```bash
   pip install pytest
   ```

2. Create a new directory called `test`
   - Init the directory with an `__init__.py`

   - Inside the test directory, create a new file called `test_example.py`

     ```python
     def test_equal_or_not_equal():
     	assert 3 == 3
     ```

   - `assert` means statement that checks if a condition is true.

3. Run Pytest
   - Run pytest in command line

     ```bash
     pytest
     ```

   - Pytest will run all tests automatically that sit within files that have the name `test` in them.

4. Check the test results

#### 159. Pytest Introduction

(Follow the instructions above)

#### 160. Pytest Basics Overview

###### Pytest Basics

In pytest, test cases are based on `assert` statements.
Each `assert` checks whether a given expression evaluates to `True`. If the expression is `False`, the test fails.

- Validate Integers

  ```python
  def test_equal():
      # Check equality and inequality
      assert 3 == 3
      assert 3 != 2
  ```

- Validate Instances

  ```python
  def test_instance():
      # Check object type using isinstance
      assert isinstance("hello", str)
      assert not isinstance("10", int)
  ```

- Validate Booleans

  ```python
  def test_boolean():
      # Check boolean expressions
      validated = True
      assert validated
      assert not ("hello" == "world")
  ```

- Validate Types

  ```python
  def test_type():
      # Verify exact data types
      assert isinstance("hello", str)
      assert isinstance(10, int)
  ```

- Validate Greater Than & Less Than

  ```python
  def test_comparison():
      # Compare numeric values
      assert 7 > 3
      assert 4 < 10
  ```

- Validate Types

  ```python
  def test_collections():
      # Test list membership and logical functions
      nums = [1, 2, 3, 4, 5]
      flags = [False, False]

      # Check if elements exist in the list
      assert 1 in nums
      assert 7 not in nums

      # all() returns True if all elements are truthy
      assert all(nums)

      # any() returns True if at least one element is truthy
      assert not any(flags)
  ```

#### 162. Pytest Object Overview

（to be continued)

## Section 15: Project 5 - Full Stack Application

#### 182. Full Stack Introduction

In section, we will build a full-stack we application.

This application will have a complete user interface. `Cookie` will also be used.

#### 183. Setup Our FastAPI Application

Add prefix and tags for our `todos` router:

```python
# Create a router instance for grouping related endpoints
router = APIRouter(
    prefix="/todos",
    tags=['todos']
)
```

#### 184. FastAPI Full Stack - Jinja Overview

In this section, we will go over `Jinja` templating.

###### What is Jinja?

- Fast, expressive and extensible templating language
- Able to write code similar to Python in the DOM
- The template is passed data to render with final results

###### What are Jinja Templating Tags and Scripts?

Jinja tags allows developers to be confident while working with backend data, using tags that are similar to HTML.

- Now image we have a list of todos that we retrieved from the database
  - We can pass the entire list of todos to the front-end

    ```python
    context: {
    "todos": todo_list
    }
    ```

  - And loop through each todo with this simple `for` loop on the template

    ```jinja2
    {% for todo in todos %}
    	Do something with todo
    {% enfor %}
    ```

  - We can use Jinja templating language with `if else` statements

    ```jinja2
    {% if todos %}
    	Display: {{ todos|length }} Todos
    {% else %}
    	You don't have any todos!
    {% endif %}
    ```

#### 185. FastAPI Full Stack - Installation of Requirements

1. Create a `templates` folder in the project root.
   - This directory is used to store all Jinja2 HTML templates.
   - FastAPI will load templates from this folder at runtime.

2. Create `home.html` in the `templates` folder.
   - This file defines the basic structure of the home page.

     ```html
     <!doctype html>
     <html lang="en">
       <head>
         <meta charset="UTF-8" />
         <title>TodoApp</title>
       </head>
       <body>
         <h1>Welcome to this FastAPI Course!</h1>
       </body>
     </html>
     ```

3. Install `jinja2`
   - Jinja2 is the template engine used for server-side rendering.

     ```bash
     pip install jinja2
     ```

4. Import required modules in `main.py`.
   - `Request` represents the current HTTP request.

   - `Jinja2Templates` provides template rendering support.

     ```python
     from fastapi import FastAPI, Request
     from fastapi.templating import Jinja2Templates
     ```

5. Initialize the template engine.
   - This configures the template loader.

   - All templates will be resolved from the `templates` directory.

     ```python
     # Initialize Jinja2 template engine
     # All HTML files should be placed in the "templates" directory
     templates = Jinja2Templates(directory="templates")
     ```

6. Render the template in a route.

   The `request` object must be included in the context for FastAPI templates.

   ```python
   # Register a GET route for the home page ("/")
   @app.get("/")
   def test(request: Request):
       # Receive the current HTTP request object
       # The request must be passed to the template context

       # Render "home.html" using Jinja2
       # Pass "request" so the template can access request data
       return templates.TemplateResponse("home.html", {"request": request})
   ```

#### 186. FastAPI Full Stack -Setup CSS

1. Create a `static` folder in the project root.
   - This directory is used to store static assets.

   - Common subfolders include `css/` and `js/`.

   - Structure example:

     ```
     static/
     ├── css/
     │   └── base.css
     └── js/
     ```

2. Create `base.css` in `css/`:

   ```css
   h1 {
     color: red;
   }
   ```

   - This file defines basic styling rules.

3. Import `StaticFiles` in `main.py`.
   - `StaticFiles` is used to serve static resources.

     ```python
     from fastapi.staticfiles import StaticFiles
     ```

4. Mount the static directory.

   ```python
   # Maps the `/static` URL path to the local `static/` folder.
   # Enables FastAPI to serve CSS, JavaScript, and images.
   app.mount("/static", StaticFiles(directory="static"), name="static")
   ```

5. After mounting, link the CSS file in `home.html`.
   - `url_for()` dynamically generates the correct static file URL.

   - Prevents hardcoding paths and improves portability.

     ```css
     <link
       rel="stylesheet"
       type="text/css"
       href="{{ url_for('static', path='/css/base.css') }}"
     />
     ```

#### 187. FastAPI Full Stack - CSS & JS

This course will use [Bootstrap](https://getbootstrap.com/) for CSS and JS.

#### 188. FastAPI Full Stack - Login Page

1. Creat `login.html` in `templates` folder

2. Link `base.css` and `bootstrap.css` in login page

   ```html
   <link
     rel="stylesheet"
     type="text/css"
     href="{{ url_for('static', path='/css/base.css') }}"
   />
   <link
     rel="stylesheet"
     type="text/css"
     href="{{ url_for('static', path='/css/bootstrap.css') }}"
   />
   ```

3. Create components in html body

   ```html
   <body>
     <div class="container">
       <div class="card">
         <div class="card-header">
           <div class="card-body">
             <form id="loginForm">
               <div class="from-group">
                 <label>Username</label>
                 <input
                   type="text"
                   class="form-control"
                   name="username"
                   autocomplete="username"
                   required
                 />
               </div>
               <div class="form-group">
                 <label>Password</label>
                 <input
                   type="password"
                   class="form-control"
                   name="password"
                   autocomplete="current-password"
                 />
               </div>
               <button type="submit" class="btn btn-primary">Login</button>
             </form>
           </div>
           <div class="card-footer text-muted">
             <a href="/auth/register-page">Register?</a>
           </div>
         </div>
       </div>
     </div>
   </body>
   ```

4. Define `render_login_page` in `auth.py`

   ```python
   from fastapi import Request
   from fastapi.templating import Jinja2Templates

   templates = Jinja2Templates(directory="templates")

   ### Pages ###
   @router.get("/login-page")
   def render_login_page(request: Request):
       return templates.TemplateResponse("login.html", {"request": request})
   ```

#### 189. FastAPI Full Stack - Register Page

Follow similar steps as log-in page, we can now build our register page.

###### Notes

Now, because of the lack of JS, none of the log-in page and register page works.

#### 190. FastAPI Full Stack - Layout Page (Inheritance)

Jinja allows us to easily be able to **reuse** a lot of the same things that we're going to need inside each of our HTML file.

1. Create a `layout.html` in `templates` folder

   `  {% block content %}  {% endblock %}` is the key.

   ```html
   <!doctype html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <link
         rel="stylesheet"
         type="text/css"
         href="{{ url_for('static', path='/css/base.css') }}"
       />
       <link
         rel="stylesheet"
         type="text/css"
         href="{{ url_for('static', path='/css/bootstrap.css') }}"
       />
       <title>TodoApp</title>
     </head>
     <body>
       {% block content %} {% endblock %}
     </body>
   </html>
   ```

2. Delete contents in `body` of `login.html` and `register.html`, place `{% include 'layout.html' %}` in the head instead.

#### 191. FastAPI Full Stack - JS Implementation

1. Link JS files to `layout.html`

   ```html
   <script src="{{ url_for('static', path='/js/jquery-slim.js') }}"></script>
   <script src="{{ url_for('static', path='/js/popper.js') }}"></script>
   <script src="{{ url_for('static', path='/js/bootstrap.js') }}"></script>
   <script src="{{ url_for('static', path='/js/base.js') }}" defer></script>
   ```

#### 192. FastAPI Full Stack - Add Todo Page

1. Create xx in `todos.py`

2. Create `todo.html` in `templates`

   ```html
   {% include 'layout.html' %}
   <div class="container">
     <div class="card text-center">
       <div class="card-header">Your Todo's</div>
       <div class="card-body">
         <h5 class="card-title">List of your todo's!</h5>
         <p class="card-text">
           Information regarding stuff that needs to be complete
         </p>
         <table class="table table-hover">
           <thead>
             <tr>
               <th scope="col">#</th>
               <th scope="col">Info</th>
               <th scope="col">Actions</th>
             </tr>
           </thead>
           <tbody>
             {% for todo in todos %} {% if todo.complete == False %}
             <tr class="pointer">
               <td>{{loop.index}}</td>
               <td>{{todo.title}}</td>
               <td>
                 <button
                   onclick="window.location.href='edit-todo-page/{{todo.id}}'"
                   type="button"
                   class="btn btn-info"
                 >
                   Edit
                 </button>
               </td>
             </tr>
             {% else %}
             <tr class="pointer alert alert-success">
               <td>{{loop.index}}</td>
               <td class="strike-through-td">{{todo.title}}</td>
               <td>
                 <button
                   onclick="window.location.href='edit-todo-page/{{todo.id}}'"
                   type="button"
                   class="btn btn-info"
                 >
                   Edit
                 </button>
               </td>
             </tr>
             {% endif %} {% endfor %}
           </tbody>
         </table>
         <a href="add-todo-page" class="btn btn-primary">Add a new todo!</a>
       </div>
     </div>
   </div>
   ```

3. Now, we can use Web UI to list todos for a specifc user

###### Note

Note now we can manually delete cookies in the broswer: `Inspect` -> `Application` -> `Cookies`

We will add a log out button to delete cookie, in the next section.

#### 193. FastAPI Full Stack -Navigation Bar

In this section, we will create a navigation bar, that is set at the very top of our web page.

1. Create `navbar.html` in `templates`

   ```html
   <div>
     <nav class="navbar navbar-expand-md navbar-dark main-color fixed-top">
       <a class="navbar-brand" href="#">Todo App</a>
       <button
         class="navbar-toggler"
         type="button"
         data-toggle="collapse"
         data-target="#navbarNav"
         aria-controls="navbarNav"
         aria-expanded="false"
         aria-label="Toggle navigation"
       >
         <span class="navbar-toggler-icon"></span>
       </button>
       <div class="collapse navbar-collapse" id="navbarNav">
         <ul class="navbar-nav">
           {% if user %}
           <li class="nav-item active">
             <a class="nav-link" href="/todos/todo-page">Home</a>
           </li>
           {% endif %}
         </ul>
         <ul class="navbar-nav ml-auto">
           {% if user %}
           <li class="nav-item m-1">
             <a
               type="button"
               class="btn btn-outline text-white"
               onclick="logout()"
               >Logout</a
             >
           </li>
           {% endif %}
         </ul>
       </div>
     </nav>
   </div>
   ```

2. Include `navbar.html` in `layout.html`

   ```html
   {% include 'navbar.html'%}
   ```

#### 194. FastAPI Full Stack - Add New Todo

1. Create `add-todo.html`

2. Add new page to `todos.py`

   ```python
   @router.get("/add-todo-page")
   async def render_todo_page(request:Request):
       try:
           user = await get_current_user(request.cookies.get("access_token"))

           if user is None:
               return redirect_to_login()

           return templates.TemplateResponse("add-todo.html", {"request": request, "user": user})

       except:
           return redirect_to_login()
   ```

#### 195. FastAPI Full Stack -Edit Todo

1. Create `edit-todo.html` in `templates`

2. Create `.prettierignore`

   ```
   templates/edit-todo.html
   ```

3. Add new page to `todos.py`

   ```python
   @router.get("/edit-todo-page/{todo_id}")
   async def render_edit_todo_page(request: Request, todo_id: int, db: db_dependency):
       try:
           user = await get_current_user(request.cookies.get("access_token"))

           if user is None:
               return redirect_to_login()

           todo = db.query(Todos).filter(Todos.id == todo_id).first()

           return templates.TemplateResponse("edit-todo.html", {"request": request, "todo": todo, "user": user})

       except Exception as e:
           return redirect_to_login()
   ```

#### 196. FastAPI Full Stack - Delete Todo

1. Create a new button in `edit-todo.html`, right under `Edit your todo`

   ```html
   <button id="deleteButton" type="button" class="btn btn-danger">
     Delete
   </button>
   ```

2. Reload `uvicorn`, this should be working

#### 197. FastAPI Full Stack - Home Page Redirection

1. Delete jinja related items in `main.py`

2. Import `status` and `RedirectResponse`

3. Redirect user when accessing `localhost:8000`

   ```python
   # Register a GET route for the home page ("/")
   @app.get("/")
   def redirect_to_todos():
       return RedirectResponse(url="/todos/todo-page", status_code=status.HTTP_302_FOUND)
   ```
