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
- Commonly used as a source for data validation in FastAPI

###### How to Use Pydantic in a POST Request

- To validate the data, we should seperate our Book object and request data.

- Create a different request model for data validation: **BookRequest**
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
