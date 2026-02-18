###### Reference

[Python Tutorial: AsyncIO - Complete Guide to Asynchronous Programming with Animations](https://www.youtube.com/watch?v=oAkLSJNr5zY&t=17s)

[AsyncIO-Animations](https://github.com/CoreyMSchafer/AsyncIO-Animations)

#### Terminology Explained

`asyncio` is a Python library for writing concurrent code using `async await` syntax.

- `await` should be used in `async` function

- Three awaitable objects
  - `coroutines`: awaitable objecy returned by a async function
  - `tasks`: handle and track coroutines by `event loop`
  - `futures` : low level, usually not used directly

Asynchroness does not mean faster, it just means we can do other things instead of waiting for network requests and database queries.

This is why `asyncio` excels in tasks involving `io-bound` elements.

`event loop`is the core of every asyncio application.

- It has the following features:
  - Run asynchronous tasks and callbacks

  - perform network IO operations

  - run subprocesses.

- It should be executed by `asyncio.run()`

#### Example 1

Only synchronous code are included in this example.

In synchronous code,

- `fetch_data(2)` need to wait `fetch_data(1)` to run
- The total time should be 3 seconds

```python
import time

def fetch_data(param):
    print(f"Do something with {param}")
    time.sleep(param)
    print(f"Done with {param}")

    return f"Result of {param}"

def main():
    result1 = fetch_data(1)
    print("Fetch 1 fully completed")

    result2 = fetch_data(2)
    print("Fetch 2 fully completed")

    return [result1, result2]


t1 = time.perf_counter()

results = main()
print(results)

t2 = time.perf_counter()
print(f"Finished in {t2 - t1:.2f} seconds")
```

###### Output

```
Do something with 1
Done with 1
Fetch 1 fully completed
Do something with 2
Done with 2
Fetch 2 fully completed
['Result of 1', 'Result of 2']
Finished in 3.01 seconds
```

#### Example 2

Note: This example **DO NOT** have concurrency

Key Point:

- use `asyncio.run` to run asynchronous functions
- `coroutine objects` do not run automatically until explicitly driven.

```python
import asyncio
import time

async def fetch_data(param):
    print(f"Do something with {param} ...")
    await asyncio.sleep(param)
    print(f"Done with {param}")
    return f"Result of {param}"

# CRITICAL: This is sequential execution
async def main():
    # These are merely "blueprints".
    # Coroutine objects are lazy; they don't do anything until explicitly driven.
    task1 = fetch_data(1)       # Create coroutine objects. They are NOT running yet.
    task2 = fetch_data(2)       # Create coroutine objects. They are NOT running yet.

    # The 'await' keyword pauses 'main()', waiting for 'task1' to finish completely.
    result1 = await task1       # It is not concurrent because there is only 1 task in event loop
    print("Task 1 fully completed")

    result2 = await task2       # 'task2' only starts to be executed here because it wasn't scheduled as a Task until now.
    print("Task 2 fully completed")

    return [result1, result2]

t1 = time.perf_counter()

# Entry point: creates the event loop and runs the main coroutine.
results = asyncio.run(main())
print(results)

t2 = time.perf_counter()
print(f"Finished in {t2 - t1:.2f} seconds")
```

###### Output

```
Do something with 1 ...
Done with 1
Task 1 fully completed
Do something with 2 ...
Done with 2
Task 2 fully completed
['Result of 1', 'Result of 2']
Finished in 3.00 seconds
```

#### Example 3

This example demonstrates cooperative concurrency using Python’s `asyncio` event loop。

Key Concepts

- `await` will suspend `main` function, to make sure always print `Task 1` before printing `Task 2`
  - `await` will tell the program what we are expecting for
  - `main` will only be awakened when it get the value expected in `await`
- However, instead of waiting idly, task 2 will be executed in event loop at the same time.
  - So, you will see `Do someting with 2` right after `Do someting with 1`

```python
import asyncio
import time

async def fetch_data(param):
    print(f"Do something with {param}...")
    await asyncio.sleep(param)
    print(f"Done with {param}")
    return f"Result of {param}"

async def main():
    # SCHEDULE: create_task submits the coroutine to the event loop immediately.
    # Both tasks start running CONCURRENTLY right here.
    task1 = asyncio.create_task(fetch_data(1))
    task2 = asyncio.create_task(fetch_data(2))

    # AWAITING: main() pauses here, but task2 is already running in the background.
    # The event loop switches between task1 and task2 while they are "sleeping".
    result1 = await task1
    print("Task 1 fully completed")

    # When we reach here, task2 has already been running for 1 second.
    # It only needs 1 more second to finish, not 2.
    result2 = await task2
    print("Task 2 fully completed")

    return [result1, result2]

t1 = time.perf_counter()

results = asyncio.run(main())
print(results)

t2 = time.perf_counter()
print(f"Finished in {t2 - t1:.2f} seconds")
```

###### Output

```
Do something with 1...
Do something with 2...
Done with 1
Task 1 fully completed
Done with 2
Task 2 fully completed
['Result of 1', 'Result of 2']
Finished in 2.00 seconds
```

#### Example 4

This example simply revert the order of task 1 and task 2 when awaiting.

It tells us:

- The event loop will run whatever that is ready
  - So, you will see `Done with 1` printed before `Done with 2`, because task 2 still waits (2 seconds)
  - However, because `await` blocks main, `Task 2 fully completed` will always printed first

```python
import asyncio
import time


async def fetch_data(param):
    print(f"Do someting with {param}...")
    await asyncio.sleep(param)
    print(f"Done with {param}")
    return f"Result of {param}"

async def main():
    task1 = asyncio.create_task(fetch_data(1))
    task2 = asyncio.create_task(fetch_data(2))

    result2 = await task2
    print("Task 2 fully completed")

    result1 = await task1
    print("Task 1 fully completed")

    return [result1, result2]

t1 = time.perf_counter()

results = asyncio.run(main())
print(results)

t2 = time.perf_counter()
print(f"Finished in {t2 - t1:.2f} seconds")
```

###### Output

```
Do someting with 1...
Do someting with 2...
Done with 1
Done with 2
Task 2 fully completed
Task 1 fully completed
['Result of 1', 'Result of 2']
Finished in 2.00 seconds
```
