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

```javascript
// Import Express and immediately create an app instance
const app = require("express")();

// In-memory object to store job progress
// key   -> jobId
// value -> progress percentage (0 ~ 100)
const jobs = {};

// =======================
// Submit a new job
// =======================
app.post("/submit", (req, res) => {
  // Create a job ID when the user submits a job
  const jobId = `job:${Date.now()}`;

  // Initialize the job with 0% progress
  jobs[jobId] = 0;

  // Start the background job (simulated)
  updateJob(jobId, 0);

  // Return the jobId to the client
  // Client will use this ID later to check job status
  res.end("\n\n" + jobId, +"\n\n");
});

// =======================
// Check job status
// =======================
app.get("/checkstatus", (req, res) => {
  // Get jobId from query string
  // Example: /checkstatus?jobId=Job:123456
  const jobId = req.query.jobId;

  // Log current job progress (debugging purpose)
  console.log(jobs[jobId]);

  // Respond with current job progress
  // If jobId does not exist, this will return "undefined"
  res.end("\n\nJobStatus:" + jobs[jobId] + "%\n\n");
});

// =======================
// Start HTTP server
// =======================
app.listen(8080, () => console.log("listening on 8080"));

// =======================
// Simulate background job execution
// =======================
function updateJob(jobId, prg) {
  // Update progress in memory
  jobs[jobId] = prg;
  console.log(`updated ${jobId} to ${prg}`);

  // If progress reaches 100%, stop recursion
  if (prg == 100) return;

  // Increase progress by 10 every 3 seconds
  // setTimeout is asynchronous and non-blocking
  this.setTimeout(() => updateJob(jobId, prg + 10), 3000);
}
```

```bash
npm init -y
npm install express
node jobs.js
```

Test using `curl`:

```bash
# Submit and get jobID
curl -X POST http://localhost:8080/submit
# job:17701********

# Polling after submitting
# The cost is network cost
curl http://localhost:8080/checkstatus?jobId=job:17701********
# JobStatus:60%

curl http://localhost:8080/checkstatus?jobId=job:17701********
# JobStatus:100%
```

#### 11. Long Polling

###### Check with You Later, BUT Talk to Me Only When It's Ready

Unlike regular polling, `long polling` keeps the request open on the server side and responds **only** when new data becomes available or a timeout occurs, reducing unnecessary requests.

- Client send a request
- Server responds immediately with a handle
- Server continues to process the request
- Client uses that handle to check for status
- Server does **NOT** reply until it has the response

###### Where request/response & polling Isn't Ideal

- A request takes long time to process
  - Upload a youtube video
- The backend want to send notifications
  - A user just logged in
- Short Polling is a good but chatty
- Meet Long polling (Kafka use it)

###### Long Polling Pros and Cons

- Pros
  - Less chatty and backend friendly
  - Client can still disconnect
- Cons
  - Not real time

###### Demo Job Status: Check if A Job is Done

```javascript
// Import Express and immediately create an app instance
const app = require("express")();

// In-memory object to store job progress
// key   -> jobId
// value -> progress percentage (0 ~ 100)
const jobs = {};

// =======================
// Submit a new job
// =======================
app.post("/submit", (req, res) => {
  const jobId = `job:${Date.now()}`; // Create a unique job ID using a timestamp
  jobs[jobId] = 0; // Initialize the job with 0% progress
  updateJob(jobId, 0); // Start the background job (simulated)

  // Return the jobId to the client
  // The client will later use this ID for long polling
  res.end("\n\n" + jobId + "\n\n");
});

// =======================
// Check job status (Long Polling)
// =======================
app.get("/checkstatus", async (req, res) => {
  console.log(jobs[req.query.jobId]);

  // Long polling:
  // The client sends a request, and the server intentionally
  // delays the response until the job is completed.
  //
  // This simulates long polling by repeatedly checking job status
  // and holding the HTTP request open.
  //
  // NOTE:
  // This while-loop is only for demonstration purposes.
  // In real applications, busy-waiting like this is inefficient
  // and should be avoided.
  while ((await checkJobComplete(req.query.jobId)) === false);

  // Once the job is complete, respond to the client
  res.end("\n\nJobStatus: Complete (" + jobs[req.query.jobId] + "%)\n\n");
});

// =======================
// Start HTTP server
// =======================
app.listen(8080, () => console.log("listening on 8080"));

// =======================
// Helper for long polling condition check
// =======================
async function checkJobComplete(jobId) {
  return new Promise((resolve, reject) => {
    // If the job is not finished yet,
    // wait for a short period before checking again
    if (jobs[jobId] < 100) {
      this.setTimeout(() => resolve(false), 1000);
    } else {
      // Job is complete, allow the long-polling request to return
      resolve(true);
    }
  });
}

// =======================
// Simulate background job execution
// =======================
function updateJob(jobId, prg) {
  jobs[jobId] = prg; // Update progress in memory
  console.log(`updated ${jobId} to ${prg}`);

  if (prg === 100) return; // Stop once the job is complete
  this.setTimeout(() => updateJob(jobId, prg + 10), 3000); // Simulate long-running work by updating progress every 3 seconds
}
```

```bash
curl -X POST http://localhost:8080/submit
# job:17701********

curl http://localhost:8080/checkstatus?jobId=job:17701********
# (wait time)
#
#
#
#
#
# JobStatus: Complete 100%
```

#### 12. Server Sent Events

###### One Request, a Very Very Long Response

`Sercer Sent Events` works with request/response (HTTP).

A response has start and end, it is still a request, but an unending response

- Client sends a request
- Server sends **logical events** as part of response
- Server never writes the end of the response
- Client parse the streams data looking for the events

###### Why Using Server Sent Events

- Limitation of request/response
  - Vanilla request/response isn't ideal for notification backend
- Client wants real time notification from backend
  - A user just logged in
  - A message is just received
- Push works but restrictive
- Server Sent Event work with Request/Response
- Designed for HTTP

###### Server Sent Events Pros and Cons

- Pros
  - Real time
  - Compatible with Request/response
- Cons
  - Clients must be online
  - Clients might not be able to handle
  - Polling is preferred for light clients
  - HTTP/1.1 problem (6 connections)

###### Demo Job Status: Chrome & Node.js

Check if a job is done with progress using SSE.

Server Side: `text/event-stream`

The stream never finished, everything send below is events.

Client Side:`EventSource` in the broswer helps us to parse the streaming events.

```javascript
/*
// =======================
// Client-side (Browser)
// =======================

// Create an EventSource connection to the server
// This sends a single HTTP request and keeps the connection open
const sse = new EventSource("http://localhost:8888/stream");

// In Chrome DevTools:
// - The request appears under Network -> EventStream
// - Response header shows "Content-Type: text/event-stream"
//
// Each message sent by the server will trigger this handler
sse.onmessage = console.log;
*/

const app = require("express")();

app.get("/", (req, res) => res.send("hello!"));

// =======================
// Server-Sent Events (SSE)
// =======================
//
// When the client sends a request to /stream:
//
// 1. The server responds with Content-Type: text/event-stream
// 2. The HTTP connection is NOT closed
// 3. The server keeps writing data to the same response
//
// This is how SSE achieves server push over HTTP

app.get("/stream", (req, res) => {
  // Tell the browser that this response is an event stream
  // This switches the client into "listening mode"
  res.setHeader("Content-Type", "text/event-stream");

  // Start sending events to the client
  // Note: we do NOT call res.end()
  send(res);
});

const port = process.env.PORT || 8888;

let i = 0;

// =======================
// Event sender
// =======================
//
// This function demonstrates the core idea of SSE:
//
// - Use res.write() instead of res.send() / res.end()
// - Each message must end with "\n\n"
// - The connection stays open indefinitely
//
// Format:
// data: <message>\n\n
//
// The browser automatically parses each chunk
// and emits a "message" event on the EventSource

function send(res) {
  // Send one SSE message to the client
  // Each call to res.write() pushes data immediately
  res.write("data:" + `hello from server ---- [${i++}]\n\n`);

  // Schedule the next message
  // This simulates server-side events happening over time
  setTimeout(() => send(res), 1000);
}

// Start the HTTP server
app.listen(port);
console.log(`Listening on ${port}`);
```

#### 13. Publish Subscribe (Pub/Sub)

###### One Publisher, Many Users

In the pub/sub model, **publishers** send messages to a topic, and **subscribers** receive messages from that topic without knowing each other.

###### Pub/Sub Pros and Cons

- Pros
  - Scales w/ multiple receivers
  - Great for microservices
  - Loose Coupling
  - Works while clients not running
- Cons
  - Message delivery issues
  - Complexity

###### RabbitMQ Demo

CloudAMQP

#### 14. Multiplexing vs Demultiplexing (h2 proxing vs Connection Polling)

###### HTTP/2, QUIC, Connection Pool, MPTCP

**Multiplexing** is the process of combining multiple independent data streams into a single shared transmission channel.
**Demultiplexing** is the reverse process of separating that shared stream back into individual streams at the receiver.

###### Connection Pooling

**Connection pooling** means keeping a pool of reusable connections so clients don’t need to create and destroy a connection for every request.

###### Browser Connection Pool Demo

Up to 6 connections in HTTP/1.1, After that we are blocked.

Using the same code in long pooling example code.

When we send more than 6 requests, we can see in `Network`, only 6 connections are established.

The protocol here is `HTTP/1.1`.

#### 15. Stateless vs Stateful

###### Is State Stored in the Backend?

**State** is memory that affects future behavior

###### Stateful vs Stateless Backend

- Stateful
  - Stores **state** about **clients** in the memory
  - Depends on the information being there
- Stateless
  - Client is **responsible** to "transfer the state" with every request
  - May store but can safely lose it

###### Stateless Backend

- Stateless backend can still store data somewhere else
- Can you restart the backend during the idle time while the client workflow continues to work?

###### What Makes a Backend Stateless?

- Stateless backends can store state somewhere else (database)
- The backend remain stateless but the **system** is stateful (database dies will lose everything, in a sense, state is held in DB, not in backend memory)

###### Stateless vs Stateful Protocols

- TCP is stateful
  - Sequences, Connection file descriptor
- UDP is stateless
  - DNS send queryID in UDP to identify queries
  - QUIC sends connectionID to identify connections
- Actually, you can build a stateless protocol on top of stateful one and vice versa, like HTTP on TCP, QUIC on UDP

###### Is There Complete Stateless System?

- Stateless systems are rare
- Examples
  - A backend service that relies completely on the input
    - Check if input param is a prime number
  - JWT (JSON Web Token)

#### 16. Sidecar Pattern

###### Thick Clients. Thicker Backends

(to be added)

## Section 3 Protocols

#### 17. Protocols Intro

What would you take into consideration when you design a protocol?

We will explore the most popular protocols, the fundamentals, HTTP/1.1, HTTP/2, etc.

#### 18. Protocol Properties

###### What to Take into Account When Designing a Protocol?

###### What is A Protocol?

- A system that allows two parties to communicate
- A protocol is designed with a set of **properties**
- Depending on the purpose of the protocols
- TCP, UDP, HTTP, gRFC, FTP

###### Protocol Properties

`Protocol Properties` is the most important part of a protocol.

Protocol Properties define how data is structured, transmitted, and identified between communicating systems.

They determine the efficiency, reliability, and usability of a protocol in real-world applications.

- Data Format
  - Text based (plain text, JSON, XML)
  - Binary (protobuf, RESP, h2, h3)
- Transfer Mode
  - Message Based (UDP, HTTP)
  - Stream (TCP, webRTC)
- Addressing System
  - DNS name, IP, MAC
- Directionality
  - Bidirectional (TCP)
  - Unidirectional (HTTP)
  - Full/Half duplex
- State
  - Stateful (TCP, gRPC, apache thrift)
  - Stateless (UDP, HTTP)
- Routing
  - Proxies, Gateways
- Flow & Congestion Control
  - TCP (Flow & Congestion)
  - UDP (No Control)
- Error Management
  - Error Code
  - Retries and timeouts

#### 19. OSI Model

###### Open System Interconnection Model

7 Layers each describe a specific networking component

- Layer 7 - Application - HTTP/FTP/gRPC
- Layer 6 - Presentation - Encoding, Serialization
- Layer 5 - Session - Connection establishment, TLS
- Layer 4 - Transport - UDP/TCP
- Layer 3 - Network - IP
- Layer 2 - Data link - Frames, Mac address Ethernet

###### Why Do We Need a Communication Model?

Without a standard model:

- Your application mush have knowledge of underlying network medium
- Upgrading network equipments becomes difficult

But with a standard model:

- Innovation can be done in each layer separately without affecting the rest of the models

###### The OSI Layers - an Example (Sender)

Example: sending a POST request to an HTTPS webpage

- Layer 7 Application
  - POST request with JSON data to HTTPS server
- Layer 6 - Presentation
  - Serialize JSON to flat byte string
- Layer 5 - Session
  - Request to establish TCP connection/TLS
- Layer 4 - Transport
  - Send SYN request target port 443
- Layer 3 - Network
  - SYN is placed an IP packet(s) and adds the source/dest IPs
- Layer 2 - Data link
  - Each packet goes into a single frame and adds the source/dest MAC addresses
- Layer 1 - Physical
  - Each frame becomes string of bits which converts into either a radio signal (wifi), electric signal (ethernet), or light (fiber)

###### The OSI Layers - an Example (Receiver)

Receiver computer receives the POST request the other way around

- Layer 1 - Physical
  - Redio, electric signal or light is received and converted into digital bits
- Layer 2 - Data link
  - The bits from Layer 1 is assembled into frames
- Layer 3 - Network
  - The frames from Layer 3 is assembled into IP packet
- Layer 4 - Transport
  - The IP packets from layer 3 are assembled into TCP segments
  - Deals with Congestion control/flow control/retransmission in case of TCP
  - If segment is SYN we don't need to go further into more layers as we are still processing the connection request
- Layer 5 - Session
  - The connection session is established or identified
  - We only arrive at this layer when necessary (three way handshake is done)
- Layer 6 - Presentation
  - Deserializing flat byte strings back to JSON for the app to consume
- Layer 7 - Application
  - Application understand the JSON POST request and your express json or apache request receive events is triggered.

###### Across Networks

Client -> Switch -> Router -> Server

A switch works at Layer 2 and forwards data using MAC addresses.

A router works at Layer 3 and forwards data using IP addresses.

A firewall works from Layer 3 to Layer 7 and controls traffic using security rules.

Port numbers and protocol headers are usually NOT encrypted。

- Source IP
- Destination IP
- Port
- TCP headers

but application data MAY be encrypted (for example with HTTPS/TLS).

- HTTP URL path
- Headers
- Body
- JSON
- Passwords
- Cookies

###### The Shortcomings of The OSI Model

- OSI model has too many layers which can be hard to comprehend
- Hard to argue about which layer does what
- Simpler to deal with layer 5-6-7 as just one layer, application

###### TCP/IP Model

TCP/IP model only has 4 layers

- Application (Layer 5, 6, 7)
- Transport (Layer 4)
- Internet (Layer 3)
- Data Link (Layer 2)
- Physical layer is not officially covered in this model

#### 24. HTTP/1.1

###### Simple Web Protocol Lasts Decades

Client/Server Architecture

- (Client) Browser, python or javascript app, or any app that makes HTTP request
- (Server) HTTP Web Server, e.g. IIS, Apache Tomcat, NodeJS, Python Tornado

###### HTTP Request

```
Method | PATH | Protocol
       Headers
        Body
```

```bash
curl -v google.com

# > GET / HTTP/1.1
# > Host: google.com
# > User-Agent: curl/8.7.1
# > Accept: */*
```

###### HTTP Response

```
Protocol | Code | Code Text
       Headers
        Body
```

```bash
curl -v google.com

# < HTTP/1.1 301 Moved Permanently
# < Location: http://www.google.com/
# < Content-Type: text/html; charset=UTF-8
...
# <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8"
# <TITLE>301 Moved</TITLE></HEAD><BODY>
# <H1>301 Moved</H1>
# The document has moved
# <A HREF="http://www.google.com/">here</A>.
# </BODY></HTML>
```

###### How HTTP Protocol Works

- The client establishes a TCP connection (and a TLS handshake for HTTPS)
- The client sends an HTTP request
- The server processes the request and sends an HTTP response
- The connection may be **kept alive** (After HTTP/1.1) for reuse or closed when no longer needed

###### Comparison between Different Versions
