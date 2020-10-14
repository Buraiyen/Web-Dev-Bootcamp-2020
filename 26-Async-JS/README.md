# Section 26: Async JavaScript. Oh boy!

## 1. The Call Stack

The Call Stack is the mechanism that the JS interpreter uses to keep track of its place in a script that calls multiple functions.

How JS "knows" what function is currently being run and what functions are called from within that function, etc.

It's like a finger in a book. Your finger is keeping track of where you are reading, or like a page number or a book mark. 

This uses the stack data structure, where it has the LIFO rule.

### 1.1 How it Works

- when a script calls a function, the interpreter adds it to the call stack and then starts carrying out the function
- any functions that are called by that function are added to the call stack further up, and run where their calls are reached
- when the current function is finished, the interpreter takes it off the stack and resumes where it left off in the last code listing

```js
const multiply = (x, y) => x * y;

const square = x => multiply(x, x);

const isRightTriangle = (a, b, c) => (
    square(a) + square(b) === square(c)
)

isRightTriangle(3, 4, 5)

// isRightTriangle(3, 4, 5)
// square(3) + square(4) === square(5)

// square(3)
// multiply(3, 3)
// 9
```

`isRightTriangle` calls `square`, which then calls `multiply`

![img1](https://github.com/Brian-E-Nguyen/Web-Dev-Bootcamp-2020/blob/26-Async-JS/26-Async-JS/img-for-notes/img1.jpg?raw=true)

From the `multiply` function, the 9 is then passed into `square`, which then passes into `isRightTriangle`

```js
9 + square(4) === square(5)
```

### 1.2 Visualizing the Call Stack

[Link to example](http://latentflip.com/loupe/?code=ZnVuY3Rpb24gbXVsdGlwbHkoeCx5KSB7CiAgICByZXR1cm4geCAqIHk7Cn0KCmZ1bmN0aW9uIHNxdWFyZSh4KSB7CiAgICByZXR1cm4gbXVsdGlwbHkoeCx4KTsKfQoKZnVuY3Rpb24gaXNSaWdodFRyaWFuZ2xlKGEsYixjKXsKICAgIHJldHVybiBzcXVhcmUoYSkgKyBzcXVhcmUoYikgPT09IHNxdWFyZShjKTsKfQoKaXNSaWdodFRyaWFuZ2xlKDMsNCw1KQ%3D%3D!!!)

Chrome-based browsers also has a debugger in the dev tools. Go to the "Sources" tab

![img2](https://github.com/Brian-E-Nguyen/Web-Dev-Bootcamp-2020/blob/26-Async-JS/26-Async-JS/img-for-notes/img2.jpg?raw=true)


## 2. WebAPI's and Single Threaded

### 2.1 Single Threads

JavaScript is single threaded. What this means is that at any given point in time, that single JS thread is running at most one line of JS code at a time. It seems that it can be problematic. It could take longer to make requests for data or to create and save data. 

Even though JS can only do one thing at a time, there are many workarounds

```js
console.log('I print first!');
setTimeout(() => {
    console.log('I print after 3 seconds!');
}, 3000);
console.log('I print second!')
```
### 2.2 Web API's

Why didn't the `setTimeout` function execute second? It's because of the _browser_ doing the work, not JS. The browser itself is not written in JS. It's written in other languages, like C++. `setTimeout` is a Web API function

Ok, but how does it work?

- browsers come with Web API's that are able to handle certain tasks in the background (like making requests or setTimeout)
- the JS call stack recognizes these Web API functiosn and passes them off to the browser to take care of. It's like JS is telling the browser "remind me in 3 seconds to finish this."
- once the browser finishes those tasks, they return and are pushed onto the stack as a callback

![img3](https://github.com/Brian-E-Nguyen/Web-Dev-Bootcamp-2020/blob/26-Async-JS/26-Async-JS/img-for-notes/img3.jpg?raw=true)

JS executes the third line of code while the browser waits for 3 seconds

### 2.3 Stack Example

[Link to example](http://latentflip.com/loupe/?code=Y29uc29sZS5sb2coIlNlbmRpbmcgcmVxdWVzdCB0byBzZXJ2ZXIhIikKc2V0VGltZW91dChmdW5jdGlvbigpIHsKICAgIGNvbnNvbGUubG9nKCJIZXJlIGlzIHlvdXIgZGF0YSBmcm9tIHRoZSBzZXJ2ZXIuLi4iKQp9LCAzMDAwKQpjb25zb2xlLmxvZygiSSBBTSBBVCBUSEUgRU5EIE9GIFRIRSBGSUxFISIp!!!)