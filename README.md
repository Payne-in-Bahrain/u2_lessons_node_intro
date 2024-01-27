![](https://i.imgur.com/hA8ZNev.png)

# Intro to Node.js

## Learning Objectives

| Students Will Be Able To |
|---|
| Explain the Use Case for Node.js |
| Use Node.js to Execute JavaScript |
| Create and Use Node Modules |

## Road Map

1. Setup
2. What is Node.js?
3. Why the Enthusiasm for Node.js?
4. Why is Node.js so Performant?
5. Node Modules
6. Practice Exercises - Node Modules
7. Further Study

## 1. Setup

We'll be writing a bit of code in VS Code in this lesson!

1. Fork and clone this repo in your GA folder. 
3. Make a new folder named first-node:  `mkdir first-node`
4. Move into the new folder:  `cd first-node`
5. Create a main.js file: `touch main.js`
6. Open the project/folder in VS Code:  `code .`

## 2. What is Node.js?

<img src="https://i.imgur.com/nXTOu8F.jpg">

**Node.js is a runtime environment that runs on the v8 javascript runtime for executing JavaScript outside of the browser!**

Node's runtime environment for JS is different than that in the browser, primarily because:
- It doesn't have the browser's DOM or [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API).
- Node has low-level networking and file system APIs that browser JS does not (for security reasons).

Node is very "lightweight", i.e., only low-level "core" modules for networking, filesystem access, etc. are built-in.

However, its functionality is extended via open source libraries called packages.  These packages are managed using the `npm` command installed with Node.

Node's package ecosystem is the largest open source ecosystem in the world.

Other Facts:

- Created in 2009 by Ryan Dahl with Joyent, Inc.
- Uses the same _V8 JavaScript Engine_ used in the Chrome browser to compile JS programs into machine code.
- In addition to being used to build high-performance web applications, Node is also a great tool for building command-line tools.
- Node is an open source project governed by the [OpenJSFoundation/Node.js Foundation](https://foundation.nodejs.org/) with board representation from companies such as:
  <img src="https://i.imgur.com/8fZqO3E.png">

### Node's REPL

A **REPL** (Read-Eval-Print Loop) is a tool used in programming that allows you to interact with a computer programming language in a dynamic and iterative way. Imagine it as a virtual playground where you can type in commands or snippets of code, and immediately see the results of their execution.

Here's a breakdown of what happens in a REPL:

- **Read:** You input a command or a piece of code into the REPL.
- **Eval:** The REPL evaluates or executes the code you entered.
- **Print:** The result of the code execution is displayed or printed on the screen.
- **Loop:** The process repeats, allowing you to input new commands or modify existing ones based on the feedback you receive.

It's like having a conversation with the computer in a step-by-step manner. This interactive nature of a REPL is especially beneficial for learning and testing small pieces of code. You can experiment, make changes on the fly, and instantly see the outcomes, which can be a great way to und

Programming languages such as Python and Ruby also have REPLs.

Let's first open an integrated Terminal in VS Code using `control + backtick`

To start [Node's interactive REPL](https://nodejs.org/api/repl.html) we type `node` in Terminal

In the REPL we can write JS and even load Node modules, which we're going to learn about in this lesson:

```
> 10 + 5
15
> function sayHello() {
... console.log('Hello');
... }
undefined
> sayHello()
Hello
undefined
> const http = require('http');
undefined
> http
[ a large JS object representing Node's 'http' module ]
```

Press `control-c` twice to exit REPL.

### Executing Node Programs

Executing a Node app is as easy as typing `node` in Terminal followed by the name of the module.  For example, if you have a module named **main.js**:

```
node main.js
```
Note that you don't need to include the ".js" file extension.
	
Yes, running a Node app is that easy!

### ❓ Review Questions - What is Node.js?

<details>
<summary>
(1) Is Node.js a programming language?
</summary>
<hr>

**No.** It is a **runtime environment** for executing JavaScript outside of the browser.

<hr>
</details>

<details>
<summary>
(2) Is <code>const el = document.getElementById('my-list');</code> a valid JavaScript statement in a Node app?
</summary>
<hr>

**No** because there is no DOM in Node.

<hr>
</details>

## 3. Why the Enthusiasm for Node.js?

First and foremost, **performance** - businesses can handle more traffic with less hardware!

Secondly, developer **synergy**. Developers can use JavaScript on both client & server, thus becoming a full-stack dev is more obtainable and companies can better utilize their developer resources across the front and back-ends.

The improvements in server performance and developer productivity result in **businesses saving money**.

Businesses saving money results in **wide adoption**.

Most importantly, wide adoption of Node.js results in strong demand for Node developers!

## 4. Why is Node.js so Performant?

[Exploring the Inner Workings of the Node.js Event Loop](https://www.devtip.co/exploring-the-inner-workings-of-the-node-js-event-loop/)


## Input/Output (I/O) and Node.js:

When a computer interacts with external systems like databases or networks, it performs Input/Output (I/O) operations. These tasks take more time than operations happening inside the computer. Properly handling I/O is crucial for performance and usability in web development.

Node.js was created to tackle I/O challenges. It's designed to be efficient by handling I/O in a non-blocking way. This means it doesn't wait for one task to finish before moving on to the next, making it great for tasks like user input, network requests, and timers.

## Event Loop in Node.js:

- **Event-Driven Nature:** Node.js applications respond to events like incoming requests or file I/O.
  
- **Event Queue:** When an asynchronous operation completes or an event occurs, a corresponding event is added to the event queue.

- **Event Loop:** The event loop is a continuous process that checks the event queue for new events.

- **Callback Execution:** Callbacks are functions that get executed in response to specific events. Node.js is non-blocking, so these callbacks are typically asynchronous tasks like reading a file or making a network request.

- **Non-Blocking Nature:** While a callback is executing, the event loop continues to check for other events. If there are no events or the current callback is synchronous, the event loop remains idle.

In simple terms, Node.js handles tasks efficiently by not waiting around. It adds events to a queue, and the event loop takes care of executing the associated tasks, allowing the server to handle many things at once without freezing up. Developers use callback functions and promises to work smoothly with Node.js' non-blocking I/O.

**Timers and Intervals**

Node.js also allows you to schedule functions to be executed after a certain period using timers (e.g., `setTimeout`) or at regular intervals (e.g., `setInterval`).

- These timer events are also managed by the event loop.

Here's a simple example to illustrate the event loop in Node.js:

```
console.log('Start');

// Asynchronous operation using setTimeout
setTimeout(() => {
  console.log('Timeout callback');
}, 1000);

// Synchronous operation
console.log('End');
```
In this example, the output will be:

```
Start
End
Timeout callback
```
This demonstrates that while the asynchronous operation (setTimeout) is waiting, the event loop continues to execute other synchronous code.

Here's an example of another real world use case that you'll see very soon:

```
async function fetchData() {
  try {
    // Asynchronously fetch data
    let result = await fetch('https://example.com/data');

    // Code here runs when the promise is resolved
    console.log('Data fetched:', result);

  } catch (error) {
    // Code here runs if the promise is rejected
    console.error('Error fetching data:', error);
  }
}
```

Understanding the event loop is essential for writing efficient and scalable Node.js applications, especially when dealing with a large number of concurrent connections. It allows you to handle many tasks simultaneously without blocking the execution of the program.

So if someone asks in an interview, when you run a script using Node, it  runs in a single thread. However, this thread can handle multiple pieces of code simultaneously by running them asynchronously in the background. So, even though it's one thread, it can manage various tasks concurrently.

If you're still having trouble understanding, think about this.  I'm teaching, I ask Michael to go get me some laban.  I'm going to continue teaching while Michael looks for the laban.  When Michael gets back with the laban, if it's the right flavor I'll say, 'Oh boy, laban!'  If not, I'll shake my head and say, 'Wrong!'  

Cool, let's learn about Node Modules...

## 5. Node Modules

Modules in Node allow us to **modularize** and **reuse** code in a Node app.

Modules can contain any number of JS functions and related data.

### Modules Built Into Node

Node itself comes with several _core modules_, such as the `http` and `fs` modules.

Let's use the core `fs` module to create a file:

```js
// main.js

const fs = require('fs');

fs.writeFile('./hello.txt', 'Hello!', function() {
  console.log('done creating file');
});
```

As we can see that the `fs` module "exports" an `object` that has methods such as `writeFile`.

### Our Own Node Modules

In a Node application, **every** JavaScript file is a module!

A Node app's modules (files) can be put in any folder within the project allowing us to create modules inside of aptly named folders, such as `models`, `routes`, `controllers`, `views`, etc.

A module is "loaded" into a Node app using Node's `require` function - just like we did to load the `fs` module. This `require` syntax is referred to as CJS(common javascript modules) and is the default in node.js. You may encounter alternative module loading syntaxes such as ESM(ECMAScript module syntax) when we begin working with react, but for right now, it's adequate just to understand that the use of `require` is typically associated with CJS module syntax.

Let's create a file/module named **days-of-week.js** by entering `touch days-of-week.js` in Terminal or by using VS Code's GUI.

Every Node module has a global `module` object - let's log it out and check out its properties:

```js
// days-of-week.js

console.log(module);
``` 

Now let's run our Node module by typing<br>`node days-of-week` in Terminal.

We're getting an inside look at how Node implements its module system:

```js
Module {
  id: '.',
  path: '/Users/username/code/first-node',
  exports: {},
  filename: '/Users/username/code/first-node/days-of-week.js',
  loaded: false,
  children: [],
  paths: [
    '/Users/username/code/first-node/node_modules',
    '/Users/username/code/node_modules',
    '/Users/username/node_modules',
    '/Users/node_modules',
    '/node_modules'
  ]
}
```

Each module is uniquely identified by its fully qualified filename (including the folder path). This allows modules to be named the same, as long as they exist in different folders.

The property on `module` that we're really interested in though is `exports`...

### `module.exports`

The `exports` property on the `module` variable is used to "export" whatever functionality should be exposed by the module...

### Exporting a Single Piece of Functionality

Whatever is assigned to `module.exports` can be accessed by any number of other modules using the `require` function we saw earlier.

Let's verify this by assigning a string to `module.exports`:

```js
// days-of-week.js

module.exports = 'SEI Rocks!';
```

Now in **main.js**, we can now put the `require` function to work:

```js
// main.js

const daysOfWeek = require('./days-of-week');
console.log(daysOfWeek);  // -> SEI Rocks!
```
Then type `node main` in Terminal to test it out!

It is convention to name the variable the same as, or similar to, the name of the module being required. 

When we require our app's own modules, we need to always provide a relative path, i.e., starting with either a `.` or `..`

<hr>

👉 **You Do:** Update `module.exports` <small>(1 min)</small>

1. Instead of exporting a string, change **days-of-week.js** to export the following array instead:

	```js
	['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa']
	```

2. Run `node main` again to check it out.

> Key Point:  `require()` returns whatever `module.exports` holds!

<hr>

If we updated 

```js
// main.js

const daysOfWeek = require('./days-of-week');
console.log(daysOfWeek);  // -> SEI Rocks!
```
to
```js
const daysOfWeek = require('./days-of-week')[1];
console.log(daysOfWeek);
```

<details>
<summary>
❓ What would be logged out?
</summary>
<hr>

**`Mo`**

<hr>
</details>

### Exporting Lot's of Functionality 

`module.exports` is initialized to an empty object by default allowing us to easily create properties on it.

Creating properties on `module.exports` is a way to expose multiple pieces of functionality.

Let's try it out:

```js	
// days-of-week.js

const weekdays = ['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa'];

module.exports.weekdays = weekdays;

module.exports.getWeekday = function(dayNo) {
  if (dayNo < 0 || dayNo > 6) dayNo = 0;
  return weekdays[dayNo];
};
```

Now let's test it in **main.js**:

```js
const daysOfWeek = require('./days-of-week');

const day = daysOfWeek.getWeekday(5);
console.log(day);
```
`Fr` should be logged out.

> Key Point:  Again, `require()` returns whatever `module.exports` is assigned or holds!

Another common approach to exporting multiple pieces of functionality like above would be to assign a new object like this:

```js	
// days-of-week.js

const weekdays = ['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa'];

module.exports = {
  weekdays,
  getWeekday
};

function getWeekday(dayNo) {
  // handle edge cases 
  if (dayNo < 0 || dayNo > 6) dayNo = 0;
  // otherwise return array at given index 	
  return weekdays[dayNo];
}
```

#### `exports` Shortcut Variable

- Node also provides a "shortcut" variable named `exports` that references that very same object that `module.exports` does.

- For example, could do this:

  ```js
  exports.weekdays = ['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa'];
  ```
  instead of:
  ```js
  module.exports.weekdays = ['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa'];
  ```

- **IMPORTANT:** It is not possible to _**assign**_ functionality to the `exports` shortcut variable because it will stop referencing `module.exports`.

#### Module Miscellaneous

- Since modules are about code reuse, they can be required an unlimited number of times throughout the application.

- Any variables declared within a module are local to the module - they do not pollute the global scope.

- The global scope in a Node application is represented by an object named `global`, **unlike the browser's ________ object**.

### ❓ Review Questions - Modules

<details>
<summary>
(1) What are modules used for in Node?
</summary>
<hr>

**Node modules are used to modularize, organize code into separate files,** making the functionality they export reusable by any other module.

<hr>
</details>

<details>
<summary>
(2) What object in a Node module can we use to attach or assign functionality to?
</summary>
<hr>

**`module.exports`**

<hr>
</details>

<details>
<summary>
(3) How many times can we <code>require</code> a module in our program?
</summary>
<hr>

**As many times as you need to**

<hr>
</details>

Assuming the following code:

```js
// add.js module
exports = function (x, y) { return x + y };
```
and
  
```js
// use the add.js module
const add = require('./add');
let sum = add(5, 10);
```

<details>
<summary>
(4) Why won't the following code work as intended?
</summary>
<hr>

**Assigning a single piece of functionality to the `exports` shortcut/convenience variable doesn't work.  We can only add properties to it.**

<hr>
</details>

## 6. Practice Exercises - Node Modules <small>(15 mins)</small>

### 💪 Modules Practice - Single Piece of Functionality

Create a module named `cool.js`:

1. That has a function named coolifier **assigned** to the `module.exports` object.
2. The function should take a single parameter.  
3. The function should console.log the string passed into it with " is cool." attached to the end. 
4. Test the module in `main.js` like this:
	
	```js
	const coolModule = require('./cool');
	coolModule.coolifier("Michael")
	```

### 💪 Modules Practice - Multiple Functionality

Create a module named `circle.js`:

1. That exports two functions, both of which have a `radius` parameter defined.
2. The functions should be named `area` & `circumference`.
3. The functions should...
	- `area`: Computes the area of a circle (radius squared X Pi), with the radius provided as an argument. 
	- `circumference`: Computes the circumference of a circle (radius X 2 X Pi), with the radius provided as an argument
4. Hint: In JS we use `Math.PI` for Pi.
5. Test the module in `main.js` like this:

	```js
	const circle = require('./circle');
	console.log( circle.area(50) );  // 7853.98...
	console.log( circle.circumference(75) );  // 471.23...
	```

## Conclusion

In the next lesson, you will use one of the most popular Node modules, `Express`, that turns Node into a capable web server!

## 7. Further Study

### npm - Node Package Manager

Node uses a package management system to distribute open-source packages called [npm](https://www.npmjs.com/) (**N**ode **P**ackage **M**anager).

Usually a package distributes a Node module, however, sometimes the package distributes a CLI instead of a module we would use in our program.

Node programs use a `package.json` file that tracks the installed modules that the app depends upon.

Tracking an application's dependencies in `package.json` removes the necessity to push the app's node modules to the projects GitHub repo - this saves **MASSIVE** file storage and bandwidth.

If you start a Node app from scratch, the first thing you should do is create the `package.json` file by entering the following command:

```
npm init
```

It's okay to accept all of the default settings.  To accept the defaults without being prompted, you can run the command as follows:

```
npm init -y
```

Now, let's use `npm` to download and install a package:

```
npm i axios
```

There is now a `node_modules` folder that contains a folder for the `request` module and its many dependencies.

There's also a new `package-lock.json` file that npm uses to track dependencies and unlike `package.json`, should not be edited.

**`package.json`** is like the blueprint for your project. It lists what your project is, what it needs to run, and other details.

**`package-lock.json`** is like a checklist created by the computer. It keeps track of exactly which versions of each tool or library your project is using, so that everyone working on the project uses the same versions.

In short, `package.json` is the plan, and `package-lock.json` is the computer's record of exactly what was built according to that plan.

Note: it's highly recommended that `node_modules` be added to your `.gitignore` file.

We can now require the `axios` module in **main.js** and make HTTP requests:

```js
// Don't specify path when module is in node_modules
const axios = require('axios');

const fetchData = async() => {
  try {
    const response = await axios.get('http://jsonplaceholder.typicode.com/users');
    console.log(response.data);
  } catch (error) {
    console.error('Error making the request:', error.message);
  }
}

// Call the async function
fetchData();
```
> Note the first parameter in the callback is `err`.<br>This "error-first" callback signature is prevalent throughout Node.

Type `node main` to try it out.

Examining the `packages.json` file reveals that it's structured something like this:

```
 {
  "name": "first_node",
  "version": "1.0.0",
  "main": "main.js",
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "description": "", 
  "dependencies": {
    "axios": "^1.6.2"
  }
}
```

The `package.json` is used to install a project's dependencies.

Installing dependencies is necessary after cloning a repo or when using starter code for a lesson. 

To demonstrate this, first delete the `node_modules` file, then...

Now we can install our app's dependencies like this:

```
npm install
```

Witness the return of `node_modules`!

### Blocking vs. Non-Blocking Code

Learn more about [Blocking/Non-Blocking, Async/Sync](http://stackoverflow.com/questions/10570246/what-is-non-blocking-or-asynchronous-i-o-in-node-js) code.

## References

[NodeJS Homepage](https://nodejs.org/)

[Node Package Manager](https://www.npmjs.com/)
