###### Reference

[Python Pydantic Tutorial: Complete Data Validation Course (Used by FastAPI)](https://www.youtube.com/watch?v=M81pfi64eeM)

[Type Hints](https://www.youtube.com/watch?v=RwH2UzC2rIo)

Data Class: [Tutorial](https://www.youtube.com/watch?v=CvQ7e6yUtnw&t=240s)

Pydantic: [Documentation](https://docs.pydantic.dev/latest/)

Pydantic AI: [Documentation](https://ai.pydantic.dev/)

## Type Hint

Notice that `type hinting` is totally different from `type checking`

For Type Checking, see [Mypy](https://mypy-lang.org/)

#### Type Hinting, Type Checking and Data Validation

Python Tutorial: [Type Hinting vs Type Checking vs Data Validation - What’s the Difference?](https://www.youtube.com/watch?v=fM4O9bModsE)

All of the three concepts are related with **types**, but they serve different purposes.

- Type Hints tells us how we expect something to be.

- Type Checking is **static analysis** that makes sure that we're sticking to our declared types.

- Data Validation happens in **runtime** and make sure that data meet our requirements

###### Type Hinting

Type Hinting and Annotation are similar concepts with slight differences.

Note that Python **ignores** type hints at runtime, it is just meta-data.

- variables
- function parameters
- return values

###### Type Checking

`Type Checking` analyze your code before running to make sure that types you specfied are correct.

It requires an **external** tool, here we use `Mypy Type Checker`, a VS Code extension.

```python
def create_user(name:str, age:int):
    return {
        "name": str,
        "age": int
    }

user1 = create_user("John", "18")
```

`mypy` will check type of parameters and report to you like this:

```
Argument 2 to "create_user" has incompatible type "str"; expected "int"
```

However, type checkers only report type mismatches to us, but **NOT** prevent code running.

We can still ignore the message above and run this code.

Also, as a static check, mypy will not guard against dynamic data, such as APIs, user input, etc.

###### Data Validation

`Data Validation` is a runtime verification that make sure data meets specific requirements. It raises validation error to make sure you know what is going wrong.

Manual Validation

```python
def create_user(name:str, age:int):
    if not isinstance(age, int):
        raise TypeError("Age should be an integer")
    return {
        "name": str,
        "age": int
    }

user1 = create_user("John", "18")
```

```
TypeError: Age should be an integer
```

Pydantic

`Pydantic` uses type hinting to do data validation, it is great for **API payloads**, **config loading**, and such data coming from external sources.

#### Type Hinting in Action

Python Tutorial: [Type Hints - From Basic Annotations to Advanced Generics](https://www.youtube.com/watch?v=RwH2UzC2rIo&t=292s)

Type Hints can be added to

- variables

  ```python
  name: str = "John"
  age: int = 38
  ```

- Function Parameter

  ```python
  def create_user(first_name:str, last_name: str, age:int):

      return {
          "first_name": first_name,
          "last_name": last_name,
          "age": age
      }

  user1 = create_user("John", "Doe", 18)
  ```

- Return Values

  ```python
  def create_user(first_name, last_name, age) -> dict:
  # ...
  ```

###### Syntax

- union

  ```
  age: int | None = None
  ```

- list

  ```
  list[int]
  ```

- dict

  ```python
  def create_user() -> dict[str, str | int | None]:
  # ...
  ```

- Type Aliases: [documentation](https://typing.python.org/en/latest/spec/aliases.html)

  ```python
  Users = dict[str, str | int | None]

  def create_user() -> Users:
  # ...
  ```

###### User-Defined Type: NewType

```python
from typing import NewType

RGB = NewType("RGB", tuple[int, int, int])

User = dict[str, str | int | RGB | None]


def create_user(first_name:str, last_name: str, age:int, fav_color: RGB | None = None) -> User:

    return {
        "first_name": first_name,
        "last_name": last_name,
        "age": age,
        "fav_color": fav_color
    }

# user1 = create_user("John", "Doe", 18, (109, 123, 134))
# RGB should be explictly identified here
user2 = create_user("John", "Doe", 18, RGB((109, 123, 134)))
```

###### TypedDict

```python
from typing import TypedDict

class User(TypedDict):
    first_name: str
    last_name: str
    email: str
    age: int | None
    fav_color: RGB | None

# User = dict[str, str | int | RGB | None]

def create_user(first_name:str, last_name: str, age:int, fav_color: RGB | None = None) -> User:
  # ...
```

Or we can achieve similar results using `dataclass`

```python
@dataclass
class User():
    first_name: str
    last_name: str
    age: int | None
    fav_color: RGB | None


def create_user(first_name:str, last_name: str, age:int, fav_color: RGB | None = None) -> User:

    # Note that here we should return User class instead of a dictionary
    return User(
        first_name=first_name,
        last_name=last_name,
        age=age,
        fav_color=fav_color
    )
```

## Data Class

`dataclasses` aims at helping you write **data-oriented** classes.

`dataclasses` - [Data Classes](https://docs.python.org/3/library/dataclasses.html)

Tutorial: [This Is Why Python Data Classes Are Awesome](https://www.youtube.com/watch?v=CvQ7e6yUtnw&t=240s)

#### Overview

###### Ordinary Class

When we want to save data in an ordinary class's attribute, we need to define `__init__` and `__repr__` properly, in order to save and check data.

```python
class User:
    def __init__(self, name: str, address:str):
        self.name = name
        self.addresss = address

    def __repr__(self):
        return f"name:{self.name}, address:{self.addresss}"

user1 = User(name="John", address="Main st.")
print(user1)
```

Results:

```
name:John, address:Main st.
```

###### Dataclass

However, `dataclass` saves us time and automatically creates `__init__` and `__repr__` methods for us.

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    address: str

user1 = User(name="John", address="Main st.")
print(user1)
```

Results:

```
User(name='John', address='Main st.')
```

#### Close Look at Dataclass

###### Field and Default Factory

`field()` is used to customize how a dataclass attribute behaves,

in which `default_factory` is used to **generate default values** dynamically.

```python
import uuid
from dataclasses import dataclass, field


def create_id():
    return str(uuid.uuid4())


@dataclass
class User:
    # Required fields (must be provided when creating an instance)
    name: str
    address: str

    # Optional field with a fixed default value
    active: bool = True

    # Use field() to customize how this attribute is created
    # default_factory let each User instance gets its own new empty list
    # and prevents different instances from sharing the same list
    email_address: list[str] = field(default_factory=list)

    # Use default_factory with a function
    # create_id() will be called every time a new User is created
    # This ensures each user gets a unique ID
    uid: str = field(default_factory=create_id)

user1 = User(name="John", address="Main st.")

# Print the object (dataclass automatically generates __repr__)
print(user1)
```

Result:

```
User(name='John', address='Main st.', active=True, email_address=[], uid='***')
```

###### Control Init and Repr Behaviors

`dataclass` also allows us to control `__init__` and `__repr__` behaviors by

- `field`
  - `init` parameter
  - `repr` parameter
- `__post_init__`
  - This method will automatically be executed after instance initialization.

```python
import uuid
from dataclasses import dataclass, field


def create_id():
    return str(uuid.uuid4())


@dataclass
class User:
    name: str
    address: str
    active: bool = True

    # Each instance gets its own empty list
    email_address: list[str] = field(default_factory=list)

    # init=False:
    #   This field is NOT included in the __init__() parameters
    #   The user cannot pass uid when creating an instance
    uid: str = field(init=False, default_factory=create_id)

    # repr=False:
    #   This field is hidden when printing the object
    # Used for internal/search purposes only
    _search_string: str = field(init=False, repr=False)

    def __post_init__(self) -> None:
        # This method is called automatically after __init__()
        # It is used to initialize fields that depend on other fields
        self._search_string = f"{self.name} {self.address}"

user1 = User(name="John", address="Main st.")

# _search_string is hidden because repr=False
print(user1)
```

Result:

```
User(name='John', address='Main st.', active=True, email_address=[], uid='***')
```

###### Freezing Dataclass

`frozen = True` will convert `dataclass` into **immutable** class.

When a dataclass is defined with `frozen=True`, its attributes cannot be reassigned after the object is created.

Note that `__post_init__` will be disabled because it will not allow adjusting attributes after initialization.

```python
import uuid
from dataclasses import dataclass, field


def create_id():
    return str(uuid.uuid4())


@dataclass(frozen=True)
class User:
    name: str
    address: str
    active: bool = True
    email_address: list[str] = field(default_factory=list)
    uid: str = field(init=False, default_factory=create_id)

user1 = User(name="John", address="Main st.")

print(user1)

# These will raise FrozenInstanceError
user1.name = "Tom"
user1.uid = "123"
```

###### Other Configuration

`kw_only` : makes all fields keyword-only in the generated `__init__`.

`match_args`: controls whether dataclass fields are used in structural pattern matching (`match-case`).

`slots`: Reduces memory usage and prevents adding new attributes by removing the instance `__dict__`.

## Pydantic

Python Pydantic Tutorial: [Complete Data Validation Course (Used by FastAPI)](https://www.youtube.com/watch?v=M81pfi64eeM&t=1098s)

Python's most famous data validation library. It's primary purpose is that data entering into our application need to meet certain expectations.

Pydantic has been used in many libraries, for example, FastAPI uses it to validate API requests and responses

#### Manual Validation vs. Pydantic

```python
def create_user(username, email, age):
    if not isinstance(username, str):
        raise TypeError("Username must be a string")
    if not isinstance(email, str):
        raise TypeError("Invalid email format")
    if not isinstance(age, int):
        raise TypeError("Age must be an integer")

    return {"username": username, "email": email, "age": age}

user1 = create_user("coreyms", "example@email.com", 38)
print(user1)

user2 = create_user("johndoe", None, "old")
print(user2)
```

```
{'username': 'coreyms', 'email': 'example@email.com', 'age': 38}
Traceback (most recent call last):
  File "/***/pydantic-tutorial/main.py", line 14, in <module>
    user2 = create_user("johndoe", None, "old")
            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/***/pydantic-tutorial/main.py", line 5, in create_user
    raise TypeError("Invalid email format")
TypeError: Invalid email format
```

In contrast, pydantic collects all the errors **at once**, instead of giving only the first error messages as manual validation did.

The sytax of pydantic is similar to [dataclass](https://docs.python.org/3/library/dataclasses.html).

```python
from pydantic import BaseModel

class User(BaseModel):
    username: str
    email: str
    age: int

user1 = User(username="coreyms", email="example@email.com", age=38)
print(user1)

user2 = User(username="johndoe", email=None, age="old")
print(user2)
```

From the error message below, we notice that

1. pydantic expose **two** validation errors simultaneously.
2. pydantic creates `__init__` methods automatically

It saves our time to identify errors, and define classes.

```
pydantic_core._pydantic_core.ValidationError: 2 validation errors for User
email
  Input should be a valid string [type=string_type, input_value=None, input_type=NoneType]
    For further information visit https://errors.pydantic.dev/2.12/v/string_type
age
  Input should be a valid integer, unable to parse string as an integer [type=int_parsing, input_value='old', input_type=str]
    For further information visit https://errors.pydantic.dev/2.12/v/int_parsing
```

[Pydantic: Migration Guide](https://docs.pydantic.dev/latest/migration/)

#### Basic Usage of Pydantic

When create a pydantic model, we create a class from `BaseModel`

The `type hint` in pydantic model will not only be suggestion, but also be validated by pydantic.

Also, each field will be `required` until a default value is specified.

```python
from pydantic import BaseModel

class User(BaseModel):
    # will be required fields
    uid: int
    username: str
    email: str
    # will be optional
    bio: str = ""
    is_active: bool = True

user = User(
    uid=123,
    username="coreyms",
    email="example@email.com"
)

print(user)
```

## Pydantic AI

Tutorial: [Build Production-Ready AI Agents in Python with Pydantic AI](https://www.youtube.com/watch?v=-WB0T0XmDrY&t=687s)

Pydantic AI is an extension of Pydantic, and it helps you to build AI-powered agents.

#### Configurations

To use Gemini, you should

- install `pydantic-ai`, or install `pydantic-ai-slim` with the `google` optional group:

  ```bash
  pip install "pydantic-ai-slim[google]"
  ```

- Set up you `.env` file

  ```
  GOOGLE_API_KEY=YOUR_KEY
  ```

- Initialize agent with your model specified

  ```python
  agent = Agent('google-gla:gemini-3-pro-preview')
  ```

#### Demo: Triage Agent

```python
import asyncio
from dataclasses import dataclass
from typing import Any

from pydantic import BaseModel, Field
from pydantic_ai import Agent, RunContext
from dotenv import load_dotenv


# ---------------------------------------------------------
# Environment Setup
# ---------------------------------------------------------
# Load environment variables (e.g. API keys, configs)
# In real projects, this is where LLM credentials come from
load_dotenv()


# ---------------------------------------------------------
# Domain Model (Mock Database Layer)
# ---------------------------------------------------------
# This section simulates a persistence layer.
# In production, this would be replaced by:
# - SQL / NoSQL DB
# - API calls
# - EMR / HIS system
#
# Purpose:
#   Provide structured domain data to the Agent.
#   Keep business data separate from AI logic.
# ---------------------------------------------------------

@dataclass
class Patient:
    id: int
    name: str
    vitals: dict[str, Any]


# In-memory mock database (for demo/testing only)
PATIENT_DB = {
    42: Patient(id=42, name="John Doe", vitals={"heart_rate": 72, "blood_pressure": "120/80"}),
    43: Patient(id=43, name="Jane Smith", vitals={"heart_rate": 65, "blood_pressure": "110/70"}),
}


class DatabaseConn:
    """
    Async database abstraction.

    This class represents the data access layer.
    All external data sources should be wrapped here,
    instead of being accessed directly by the Agent.
    """

    async def patient_name(self, id: int) -> str:
        patient = PATIENT_DB.get(id)
        return patient.name if patient else "Unknown Patient"

    async def latest_vitals(self, id: int) -> dict[str, Any]:
        patient = PATIENT_DB.get(id)
        return patient.vitals if patient else {"heart_rate": 0, "blood_pressure": "N/A"}


# ---------------------------------------------------------
# Dependency Injection Layer
# ---------------------------------------------------------
# This section defines what "context" the Agent depends on.
#
# Purpose:
#   - Decouple Agent logic from concrete implementations
#   - Make testing / mocking easier
#   - Support multi-user / multi-session scenarios
# ---------------------------------------------------------

@dataclass
class TriageDependencies:
    patient_id: int
    db: DatabaseConn


# ---------------------------------------------------------
# Output Schema (Structured AI Result)
# ---------------------------------------------------------
# This section defines what the LLM is allowed to return.
#
# Purpose:
#   - Enforce structured output
#   - Reduce hallucination
#   - Make downstream automation possible
# ---------------------------------------------------------

class TriageOutput(BaseModel):
    response_text: str = Field(description="Message to the patient")
    escalate: bool = Field(description="Should escalate to a human nurse")
    urgency: int = Field(description="Urgency level from 0 to 10", ge=0, le=10)


# ---------------------------------------------------------
# Agent Definition
# ---------------------------------------------------------
# This is the core AI component.
#
# Purpose:
#   - Bind LLM + Dependencies + Output Schema
#   - Define high-level behavior via system prompt
#   - Act as the orchestrator of tools and reasoning
# ---------------------------------------------------------

triage_agent = Agent(
    "google-gla:gemini-2.5-flash",
    deps_type=TriageDependencies,
    output_type=TriageOutput,
    system_prompt=(
        "You are a triage assistant helping patients. "
        "Provide clear advice and assess urgency. "
        "Please check the name with your patient and inform his/her vitals."
    ),
)


# ---------------------------------------------------------
# Dynamic System Prompt Extension
# ---------------------------------------------------------
# This function injects runtime context into the system prompt.
#
# Purpose:
#   - Personalize model behavior per request
#   - Provide grounding information
#   - Reduce hallucination
# ---------------------------------------------------------

@triage_agent.system_prompt
async def add_patient_name(ctx: RunContext[TriageDependencies]) -> str:
    patient_name = await ctx.deps.db.patient_name(id=ctx.deps.patient_id)
    return f"The patient's name is {patient_name!r}."


# ---------------------------------------------------------
# Tool Definition (LLM-Callable Function)
# ---------------------------------------------------------
# Tools expose trusted functions to the LLM.
#
# Purpose:
#   - Allow the model to fetch real data
#   - Prevent guessing / fabrication
#   - Bridge LLM reasoning and external systems
# ---------------------------------------------------------

@triage_agent.tool
async def latest_vitals(ctx: RunContext[TriageDependencies]) -> dict[str, Any]:
    """Returns the patient's latest vital signs."""
    return await ctx.deps.db.latest_vitals(id=ctx.deps.patient_id)


# ---------------------------------------------------------
# Application Entry Point
# ---------------------------------------------------------
# This section wires everything together.
#
# Purpose:
#   - Initialize dependencies
#   - Run the Agent
#   - Handle the final output
# ---------------------------------------------------------

async def main() -> None:
    # Initialize request-specific dependencies
    deps = TriageDependencies(
        patient_id=43,
        db=DatabaseConn(),
    )

    # Run the agent with user input and dependencies
    result = await triage_agent.run(
        "I have chest pain and trouble breathing.",
        deps=deps,
    )

    # Structured output validated by Pydantic
    print(result.output)


if __name__ == "__main__":
    asyncio.run(main())
```

Result:

```
response_text="Jane Smith, I understand you're experiencing chest pain and trouble breathing. Your latest vitals indicate your blood pressure is 110/70 and your heart rate is 65. Even with these readings, your symptoms are concerning and require immediate medical attention. We are escalating this to a human nurse who will contact you shortly. Please try to remain calm and avoid any strenuous activity."
escalate=True
urgency=9
```
