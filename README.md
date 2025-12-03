#node-basis
1. Modules: Exporting & Importing
Demonstrates how to share code between files using CommonJS modules.

math.js
function add(a, b) { ... }: Defines a simple function that returns the sum of two numbers.
function subtract(a, b) { ... }: Defines a function that returns the difference between two numbers.
module.exports = { add, subtract };: Objects exported here become available to other files. We are packaging add and subtract together.

app.js
const { add, subtract } = require('./math');: Imports the functions. require('./math') loads the file, and { add, subtract } extracts specific functions (object destructuring).
console.log(...): prints the result of calling the imported add and subtract functions with arguments 10 and 5.

2. File System: Blocking vs Non-Blocking
Demonstrates the difference between synchronous (blocking) and asynchronous (non-blocking) code execution.
readBlocking.js (Synchronous)
const fs = require('fs');: Imports the built-in Node.js File System module.
try { ... } catch (err) { ... }: Error handling block. If the file doesn't exist, it jumps to catch.
const data = fs.readFileSync('sample.txt', 'utf8');: Blocking operation. The code stops here and waits until the entire file is read before moving to the next line.
console.log(data);: Prints the file content only after the read is finished.
readNonBlocking.js (Asynchronous)
fs.readFile(..., (err, data) => { ... });: Non-blocking operation. Starts reading the file in the background and immediately moves to the next line of code. It does not wait.
(err, data) => { ... }: This is the callback function. It runs only when the file reading is finished.
if (err) return;: Inside the callback, we check for errors first.
console.log("This line executes before...");: This runs immediately after fs.readFile starts, proving the code didn't stop to wait for the file.

3. Async/Await: Simulating Data Fetching
Demonstrates handling asynchronous operations cleanly using Promises.
script.js
function fetchUserData() { ... }: A function simulating an API call.
return new Promise((resolve) => { ... });: Creates a Promise object. A Promise represents a future value (success or failure).
setTimeout(() => { ... }, 2000);: Waits for 2000 milliseconds (2 seconds) to simulate network delay.
resolve({ id: 1, ... });: Marks the Promise as "successful" and passes the user data back.
async function getUser() { ... }: The async keyword allows usage of await inside this function.
const user = await fetchUserData();: Pauses the execution of this function only until fetchUserData finishes and returns the data.
console.log("User:", user);: Runs only after the data has been received.
