###### Reference

[Fundamentals of Backend Engineering](https://www.udemy.com/course/fundamentals-of-backend-communications-and-protocols/?src=sac&kw=fundamentals+of+backend)

## Section 1. Introduction

#### 1. Welcome

Certain pattern in backend development.

The protocol, how communication is happenning.

The most common protocols are introduced in the course.

Understanding what is behind the scene, instead of only using library or framework.

#### 2. Who is This Course For?

This course is for those engineer who would like to know why the application works.

#### 3. Course Outline

The first section of the course, **Backend Design Patterns** will be discussed.

How client communicate with the backend, asynchronous vs. synchronous, stateful vs. stateless, sidecar pattern.

Next, **protocol** is discussed.

Rules, properties of protocol, HTTP/1.1, 2, 3, HTTPS, etc.

Because **HTTPS** is super important, a section will be discussing HTTPS.

**Backend Execution Patterns** explains how does backend executes and interacting with kernel, like taking data, etc.

Then, **Proxying and Load Balancing** will help you understand how proxy works.

#### 4. Course Notes

It is **alright** to not knowing concept at the very beginning.

## Section 2: Backend Communication Design Patterns

#### 6. Backend Communication Design Patterns Intro

There are patterns emerging when building backends.

#### 7. Request Response

We start with the most famous communication design pattern for the backend, `request-response`.

This pattern is classic, simple and everywhere. See [Request-resonse Wiki Page](https://en.wikipedia.org/wiki/Request%E2%80%93response).

###### Resquest Response Model

- Client sends a Request
- Server parses the Request
- Server processes the Request
- Server sends a Response
- Client parses the Response and consume

###### Where is This Used?

- Web, HTTP, DNS, SSH
- RPC (remote procedure call)
- SQL and Database Protocols
- APIs (REST/SOAP/GraphQL)
- Inplemented in Variations

###### Anatomy of a Request/Response

- A request structure is defined by both client and server

The client and server should **agree** on the request structure.

However, this work has been done for us, by libraries, such as requests in Python.

- Request has a boundary
- Defined by a protocol and message format
- Same for the response

HTTP Request

```
GET / HTTP/1.1
Headers
<CRLF>
BODY
```

###### Example: Sending Image with request response

Actually, the **style** of execution can change.

There are two ways to do this:

1. Send large request with the image (simple)
2. Chunk image and send a request per chunk (resumable)

###### Does not Work Everywhere

- Notification Service
  - Because request-response pattern require client to start first, is does not work when backend would like to nofity the users.
- Chatting Application
- Very Long Requests
- What if client disconnect

###### Demo: curl

The `curl` command sends an HTTP request to `http://google.com`.

- The `-v` (verbose) option prints high-level details of the request and response to the terminal, including the HTTP headers and connection steps.
- The `--trace out.txt` option records a complete byte-level trace of the network communication, capturing exactly what data is sent to and received from the server.

The trace is written to the file `out.txt`.

```bash
curl -v --trace out.txt http://google.com
cat out.txt
```

`=>` means a request,

`<=` means a response, multiple headers are returned here.

Because it is a GET request, no body is provided here.

```
== Info: Host google.com:80 was resolved.
...
== Info:   Trying [IPv6 address]:80...
== Info: Connected to google.com (IPv6 address) port 80
=> Send header, 73 bytes (0x49)
0000: 47 45 54 20 2f 20 48 54 54 50 2f 31 2e 31 0d 0a GET / HTTP/1.1..
0010: 48 6f 73 74 3a 20 67 6f 6f 67 6c 65 2e 63 6f 6d Host: google.com
0020: 0d 0a 55 73 65 72 2d 41 67 65 6e 74 3a 20 63 75 ..User-Agent: cu
0030: 72 6c 2f 38 2e 37 2e 31 0d 0a 41 63 63 65 70 74 rl/8.7.1..Accept
0040: 3a 20 2a 2f 2a 0d 0a 0d 0a                      : */*....
== Info: Request completely sent off
<= Recv header, 32 bytes (0x20)
0000: 48 54 54 50 2f 31 2e 31 20 33 30 31 20 4d 6f 76 HTTP/1.1 301 Mov
0010: 65 64 20 50 65 72 6d 61 6e 65 6e 74 6c 79 0d 0a ed Permanently..
...
<= Recv data, 219 bytes (0xdb)
0000: 3c 48 54 4d 4c 3e 3c 48 45 41 44 3e 3c 6d 65 74 <HTML><HEAD><met
0010: 61 20 68 74 74 70 2d 65 71 75 69 76 3d 22 63 6f a http-equiv="co
0020: 6e 74 65 6e 74 2d 74 79 70 65 22 20 63 6f 6e 74 ntent-type" cont
0030: 65 6e 74 3d 22 74 65 78 74 2f 68 74 6d 6c 3b 63 ent="text/html;c
0040: 68 61 72 73 65 74 3d 75 74 66 2d 38 22 3e 0a 3c harset=utf-8">.<
0050: 54 49 54 4c 45 3e 33 30 31 20 4d 6f 76 65 64 3c TITLE>301 Moved<
0060: 2f 54 49 54 4c 45 3e 3c 2f 48 45 41 44 3e 3c 42 /TITLE></HEAD><B
0070: 4f 44 59 3e 0a 3c 48 31 3e 33 30 31 20 4d 6f 76 ODY>.<H1>301 Mov
0080: 65 64 3c 2f 48 31 3e 0a 54 68 65 20 64 6f 63 75 ed</H1>.The docu
0090: 6d 65 6e 74 20 68 61 73 20 6d 6f 76 65 64 0a 3c ment has moved.<
00a0: 41 20 48 52 45 46 3d 22 68 74 74 70 3a 2f 2f 77 A HREF="http://w
00b0: 77 77 2e 67 6f 6f 67 6c 65 2e 63 6f 6d 2f 22 3e ww.google.com/">
00c0: 68 65 72 65 3c 2f 41 3e 2e 0d 0a 3c 2f 42 4f 44 here</A>...</BOD
00d0: 59 3e 3c 2f 48 54 4d 4c 3e 0d 0a                Y></HTML>..
== Info: Connection #0 to host google.com left intact
```

#### 8. Synchronous vs Asynchronous Workloads

###### Can I Do Work While Waiting?

The key question is whether execution is blocked while waiting for an external operation (e.g., I/O, network, disk).

- **Synchronous** workloads wait for completion before continuing,
- whereas **asynchronous** workloads overlap waiting time with useful work.

Synchronicity is a **client property**.

Most modern client libraries are asynchronous.

###### Synchronous I/O

- Caller sends a request and **blocks**
- Caller can not execute any code meanwhile
- Receiver responds, Caller unblocks
- Caller and Receiver are in "sync"

###### Example of an OS Synchronous I/O

- Program asks OS to read from disk
- Program main thread is taken off of the CPU
- Read completes, program can resume execution

```javascript
// Program starts
// Program uses CPU to execute stuff
doWork();
// Program reads from disk
// Program can't do anything until file loads
readFile("largefile.dat");
// Program resumes
doWork2();
```

###### Asynchronous I/O

- Caller sends a request
- Caller can work until it gets a response
- Caller either:
  - Checks if the response is ready (epoll)
  - Receiver calls back when it's done (io_uring)
  - Spins up a new thread that blocks
- Caller and receiver are not necessary in sync

###### Example of an OS Asynchronous Call (Node.js)

- Program spins up a secondary thread
- Secondary thread reads from disk, OS blocks it
- Main program still running and executing code
- Thread finish reading and calls back main thread

```javascript
// Program starts
// Program uses CPU to execute stuff
doWork();
// Program requests read from disk
// Program asks to callback when done
// Program moves on to doWork2
readFile("largefile.dat", onReadFinished(theFile));
// file is probably not read yet
// Program happy doing stuff
doWork2();
// someone just called onReadFinished
// processing it.
---->onReadFinished(theFile);
```

###### Asynchronous Workload is Everywhere

- Asynchronous Programming (promises/futures)
  - avoid blocking threads while waiting for I/O
- Asynchronous Backend Processing (queue and job_id)
  - avoid blocking requests on long-running work
- Asynchronous Commits in Postgres
- Asynchronous IO in Linux (poll, io_uring)
- Asynchronous Replication
- Asynchronous OS sync (fs cache)

###### Demo: Node.js

```javascript
const fs = require("fs");

// Step 1: This log runs immediately
console.log("1");

// Step 2: Synchronous file read
// - The current thread is BLOCKED here
// - Node.js will NOT execute any other JavaScript
//   until the file is fully read from disk
const res = fs.readFileSync("test.txt");

// Step 3: This log only runs AFTER the file read completes
console.log("file" + res);

// Step 4: This log is delayed by the blocking I/O above
console.log("2");
```

Results:

```bash
node sync.js
# 1
# filelorem
# 2
```

```javascript
const fs = require("fs");

// Step 1: Runs immediately
console.log("1");

// Step 2: Asynchronous file read
// - The file read is OFFLOADED to the OS / thread pool
// - The current JavaScript thread is NOT blocked
// - Execution continues immediately after this call
fs.readFile("test.txt", (err, data) => {
  // Step 4: This callback runs LATER,
  // after the file has been read from disk
  console.log(data.toString());
});

// Step 3: This runs BEFORE the file read completes
console.log("2");
```

```bash
node async.js
# 1
# 2
# lorem
```

#### 9. Push

###### I Want It as Soon as Possible

In a push model, the server initiates the response as soon as data is ready,rather than waiting for the client to repeatedly request it.

###### Request/response Isn't Always Ideal

- Client wants real time notification from backend
  - A user just logged in
  - A message is just received
- Push model is good for some usecase

###### What is Push

- A bidirectional connection is established between **client** and **server**
- Server **sends** data to the client, when **getting message**
- Client doesn't have to request anything

Push is used by like, RabbitMQ.

###### Push Pros and Cons

- Pros
  - Real time
- Cons
  - Clients must be online
  - Clients might not be able to handle
  - Requires a bidirectional protocol
  - Polling is preferred for light clients

#### 10. Polling

###### Request is Taking a While, I will Check with You Later.

- Client sends a request
- Server responds immediately with a **handle**
- Server continues to process the request
- Client uses that handle to check for status
- Multiple **"short"** request response as polls

###### Use Case: Where request/response isn't Ideal

- A request takes long time to process
  - Upload a youtube video
- The backend want to sends notifications
  - A user just logged in

###### Short Polling Pros and Cons

- Pros
  - Simple
  - Good for long running requests
  - Client can disconnect
- Cons
  - Too chatty (too many short requests when there are thousands users)
  - Network Bandwidth
  - Wasted Backend resources

###### Demo Job Status: curl and Node.js
