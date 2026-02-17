Agent Development Kit (ADK)

###### Reference

[Agent Development Kit (ADK) Masterclass: Build AI Agents & Automate Workflows (Beginner to Pro)](https://www.youtube.com/watch?v=P4VFL9nIaIA&list=PLQdhkr4teZUodsAhEJ2j0tTMsZOefjam4)

[GitHub Repo](https://github.com/bhancockio/agent-development-kit-crash-course)

12 different examples to walk through in this course.

#### 1. Basic Agent

Understaning the core principal of creating agents inside ADK.

###### Review Agent

`root_agent` is the entrypoint of it, make sure to have at lease **one** of it in each project.

Important properties include:

- `name`
- `model`: models such as `gemini-2.5-flash`
  - All available models: [Gemini Models](https://ai.google.dev/gemini-api/docs/models)
- `description`: Important, it helps agent to decide who a specific task should be assigned to.
- `instruction`: To tell the agent what should do and how they should do.

###### Folder Structure

ADK requires a specific format to run your agent.

```
1-basic-agent/
└── greeting_agent/
    ├── __init__.py
    ├── .env
    └── agent.py
```

###### Source Code

`.env`

```
GOOGLE_GENAI_USE_VERTEXAI=FALSE
GOOGLE_API_KEY=YOUR_KEY
```

`__init__.py`

```python
from . import agent
```

`agent.py`

```python
from google.adk.agents import Agent

root_agent = Agent(
    name="greeting_agent",
    model="gemini-2.5-flash",
    description="Greeting Agent",
    instruction="""
    You are a helpful assistant that greets the user.
    Ask for the user's name and greet them by name.
    """
)
```

###### Set Python Environment

See documentation of ADK:

- [PyPI](https://pypi.org/project/google-adk/)
- [Agent Development Kit](https://google.github.io/adk-docs/)
- [GitHub: Samples](https://github.com/google/adk-samples)
- [Web UI](https://github.com/google/adk-web)

`requirements.txt`

Note: `google-adk` has been updated because it is outdated.

```
google-adk[database]==0.3.0
yfinance==0.2.56
psutil==5.9.5
litellm==1.66.3
google-generativeai==0.8.5
python-dotenv==1.1.0
```

In root directory:

```
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

###### Get Your API Key

1. Create an account in Google Cloud
2. Create a project: `deploy-adk-quickstart`
3. Go to [Google AI Studio](https://aistudio.google.com/) and create an API Key in your project
4. Open `.env` file and replace the placeholder with your key

###### Run Agent

1. Change directory (cd) to `1-basic-agent`

2. Run the following command to check Agent Development Kit

   ```bash
   # Run the CLI tool for using Agent Development Kit
   # This command will show all the different options that you can run
   adk

   #  Agent Development Kit CLI tools.

   # Options:
   #  --version  Show the version and exit.
   #  --help     Show this message and exit.

   # Commands:
   #  api_server   Starts a FastAPI server for agents.
   #  conformance  Conformance testing tools for ADK.
   #  create       Creates a new app in the current folder with prepopulated agent template.
   #  deploy       Deploys agent to hosted environments.
   #  eval         Evaluates an agent given the eval sets.
   #  eval_set     Manage Eval Sets.
   #  migrate      ADK migration commands.
   #  run          Runs an interactive CLI for a certain agent.
   #  web          Starts a FastAPI server with Web UI for agents.
   ```

3. Run the web UI of ADK

   ```bash
   adk web
   ```

#### 2. Tool Agent

###### Type of Tools

1. Function Tools
   - Functions/Methods: define standard synchronous functions or methods in your code
   - Agent-as-Tools: Use another, potentially specialized, agent as a tool for a parent agent
   - Long Running Function Tools: Support for tools that perform asynchronous operations or take significant time to complete

2. Built-in Tools:
   - Google Search, Code Execution, Retrieval-Augumented Generation (RAG)
   - Only work with Gemini Models

3. Third-Party Tools
   - Integrate tools seamlessly from popular external libraries.
   - Examples: LangChain Tools, CrewAI Tools

###### Add Tools to Your Agents

Two tools will be used in this section:

- [Google Search](https://google.github.io/adk-docs/integrations/google-search/)
  - `google_search` as build-in tool
- Function Tool
  - `get_current_time`: To get current time

###### Source Code

```python
from datetime import datetime
from google.adk.agents import Agent
from google.adk.tools import google_search

def get_current_time() -> dict:
    """
    Get the current time in the format YYYY-MM-DD HH:MM:SS
    """
    return {
        "current_time": datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    }

root_agent = Agent(
    name="tool_agent",
    model="gemini-2.5-flash",
    description="Tool Agent",
    instruction="""
    You are a helpful assistant that can use the following tools:
    - get_current_time
    """,
    # tools=[google_search]
    tools=[get_current_time]
)
```

###### Best Practice & Limitation

1. A well-written and comprehensive **docstring** is crucial for the LLM to understand how to use the tool effectively.

2. Give type hint and exclude default value

   ```python
   def ger_current_time(format: str) -> dict:
   ```

3. Give clear return value with explanation
   - Return current time in key-value pairs

   - The preferred return type for a Function Tool is a **dictionary** in Python, a **Map** in Java, or an **object** in TypeScript. This allows you to structure the response with key-value pairs, providing context and clarity to the LLM.

     ```python
     # Use this version
     return {
     	"current_time": datatime.now.strftime("%Y-%m-%d %H:%M:%S")
     }

     # Instead of
     return datatime.now.strftime("%Y-%m-%d %H:%M:%S")
     ```

###### Showtool Calling in Action

With Google Search Tool:

> Hey! Do you have any news about Tesla this week?

With Custom Tool (get_current_time):

> Hey! What is the current time?

#### 3. Lite LLM Agent (Skipped)

Bring your own models to ADK, by using `model` parameter in `Agent`

###### Review Technologies to Connect to Other Models

- LiteLLM:
  - See docs: [GitHub](https://github.com/BerriAI/litellm), [Official Website](https://www.litellm.ai/)
- OpenRouter

###### Review Agent Code

...

###### Run Agent

...

#### 4. Structured Outputs

Enable agent to spill out structured outputs, in order to pass to APIs and other agents.

###### Review Structured Output Docs

See official docs: [Structuring Data](https://google.github.io/adk-docs/agents/llm-agents/#structuring-data-input_schema-output_schema-output_key)

`output_schema`:

- Define a schema representing the desired **output structure**. If set, the agent's final response _must_ be a **JSON** string conforming to this schema.
- Make sure you explicitly explain your schema in `instruction`, to aviod that your agent does not understand how to fill data into JSON.

`output_key`:

- A string key that response will be automatically saved to the **session's state** dictionary under it.

###### Review Agents with Structured Outputs

`agent.py`

```python
from google.adk.agents import LlmAgent
from pydantic import BaseModel, Field

# --- Define Output Schema --- #
class EmailContent(BaseModel):
    subject: str = Field(
        description="The subject line of the email. Should be concise and descriptive"
    )
    body: str = Field(
        description="The main content of the email. Should be well-formatted with proper greeting, paragraphs and signiture."
    )

# --- Create Email Generator Agent --- #
root_agent = LlmAgent(
    name="email_agent",
    model="gemini-2.5-flash",
    # Make sure to tell agent what value should be put into
    # what key in structured output (JSON)
    instruction="""
    You are an Email Generation Assistant.
    Your task is to generate a professional email based on the user's request.

    GUIDELINES:
    - Create an appropriate subject line (concise and relevant)
    - Write a well-structured email body with:
        * Professional greeting
        * Clear and concise main content
        * Appropriate closing
        * Your name as signiture
    - Suggest relevant attachments if applicable (empty list if none needed)
    - Email tone should match the purpose (format for business, friendly for colleagues)
    - Keep email concise but complete

    IMPORTANT: Your response MUST be valid JSON matching this structure:
    {
    "subject": "Subject line here",
    "body": "Email body here with proper paragraphs and formatting",
    }

    DO NOT include any explanations or additional text outside the JSON response.
    """,
    description="Generates professional emails with structured subject and body",
    output_schema=EmailContent,     # Enforce JSON output
    output_key="email",             # Store result in state['email']
)
```

###### Run Agents

Examples:

> Question:
>
> Hey! Please write an email to my wife Karly, to see if she is available for coffee tomorrow morning.
>
> Agent Response:
>
> {"subject": "Coffee Tomorrow Morning?", "body": "Hi Karly,I hope you're having a great day.I was wondering if you might be free for coffee tomorrow morning? Let me know if that works for you and if you have any preferred time or place.Looking forward to hearing from you.Best,Your Name"}

Further, since we used `output_key`, we can see the following contents in `State`:

> email:
> subject: "Coffee Tomorrow Morning?"
> body: "Hi Karly,I hope you're having a great day.I was wondering if you might be free for coffee tomorrow morning? Let me know if that works for you and if you have any preferred time or place.Looking forward to hearing from you.Best,Your Name"

#### 5. Sessions and Memory

In this section, some **core** components are introduced.

Enable agent to memorize things between different conversations.

###### Overview of Session, State & Runner in ADK

So far, `adk web` handles sessions, state, and runners for us.

- We can check the session ID in the UI
- In the sidebar, we can check state
- Also, everytime we input something in the chatbox, runner helps us to bring every part together.

[Session](https://google.github.io/adk-docs/sessions/): stateful chat history

- A `session` is nothing more than two pieces of information
  - State: key-value pair
  - Events: Everything that happened between us and agent
    - message history
    - Tool calling
  - Also, session has `id`, `app_name`, `user_id`, and `last_update_time`
- Session service has different forms:
  - InMemorySessionService
  - DatabaseSessionService
  - VertexAISessionService

Runner: the engine

- Runner usually requires two parts:
  - Agent
  - Session

###### Code Review

Structure Change:

1. `.env` moved to root folder of agent
   - Because we no longer need `adk web` to take care of environment variables, we will move the .env to root directory
     - Note that previously, `adk web` store our session data under `.adk` folder as `sesssion.db`
     - Note that this DB can be opened by `sqlite`
   - `load_env` is used to export environment variables
2. Use `{variable_name}` to extract variables defined in `state` into instruction.
   - Since we will initialized state in runners, we can fill its value to instruction using the syntax `{variable_name}`

`agent.py`:

```python
from google.adk.agents import Agent

questing_answering_agent = Agent(
    name="question_answering_agent",
    model="gemini-2.5-flash",
    description="Question answering agent",
    instruction="""
    You are a helpful assistant that answers questions about the user's preference.

    Here is some information about the user:
    Name:
    {user_name}
    Preferences:
    {user_preferences}
    """
)
```

`basic_stateful_sesstion.py`

```python
import uuid
import asyncio

from dotenv import load_dotenv
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.genai import types

from question_answering_agent import question_answering_agent


# ====================
# Config Section
# ====================

APP_NAME = "Brandon Bot"
USER_ID = "brandon_hancock"

INITIAL_STATE = {
    "user_name": "Brandon Hancock",
    "user_preferences": """
        I like to play Pickleball, Disc Golf, and Tennis.
        My favorite food is Mexican.
        My favorite TV show is Game of Thrones.
        Loves it when people like and subscribe to his YouTube channel.
    """,
}


# ====================
# App Logic
# ====================

load_dotenv()


async def main():

    session_service = InMemorySessionService()

    session_id = str(uuid.uuid4())

    await session_service.create_session(
        app_name=APP_NAME,
        user_id=USER_ID,
        session_id=session_id,
        state=INITIAL_STATE,
    )

    print("CREATED NEW SESSION:")
    print(f"\tSession ID: {session_id}")

    print("==== Running Agent ====")
    runner = Runner(
        agent=question_answering_agent,
        app_name=APP_NAME,
        session_service=session_service,
    )

    new_message = types.Content(
        role="user",
        parts=[types.Part(text="What is Brandon's favorite TV show?")],
    )

    for event in runner.run(
        user_id=USER_ID,
        session_id=session_id,
        new_message=new_message,
    ):
        if event.is_final_response():
            if event.content and event.content.parts:
                print(f"Final Response: {event.content.parts[0].text}")

    print("==== Session Event Exploration ====")
    session = await session_service.get_session(
        app_name=APP_NAME,
        user_id=USER_ID,
        session_id=session_id,
    )

    print("\n=== Final Session State ===")
    for key, value in session.state.items():
        print(f"{key}: {value}")


if __name__ == "__main__":
    asyncio.run(main())

```

###### Run Code

When we run our sample, we would expect to see the following outputs:

```bash
python basic_stateful_session.py

# CREATED NEW SESSION:
#         Session ID: ****

# ==== Running Agent ====
# Final Response: Brandon's favorite TV show is Game of Thrones.

# ==== Session Event Exploration ====
# === Final Session State ===
# user_name: Brandon Hancock
# user_preferences:
#         I like to play Pickleball, Disc Golf, and Tennis.
#         My favorite food is Mexican.
#         My favorite TV show is Game of Thrones.
#         Loves it when people like and subscribe to his YouTube channel.
```

#### 6. Persistent Storage

Allow agent to save data to database, so it can remember after rebooting.

###### Review the Code

###### Run the Example Code

#### 7. Multi-Agent

Agents working together as a multi-agent solution.

#### 8. Stateful Multi-Agent

Sharing sessions in multi-agent solution.

#### 9. Callbacks

Callbacks allow you to control every part of agent cycle.

#### 10. Sequential Agent

This section, including the following two sections, focus on the the specific workflows of agents.

Agents always work in a sequence.

#### 11. Parallel Agent

#### 12. Loop Agent
