# Section 28: AJAX and API's

## 1. Intro to AJAX

AJAX is an acronym with the following terms

- ***A***synchronous
- ***J***avaScript
- ***A***nd
- ***X***ML

This refers to a concept of loading or sending information on a given website or application. Like on reddit, you get new posts as you constantly scroll. Requests are being made to reddit to load more posts.

Instead of retrieving HTML, CSS, and JS, we would be receiving data, like in JSON or XML.

The idea of AJAX is creating apps where using JS, you can load, fetch, save, or send data

## 2. Intro to API's

***A***pplication ***P***rogramming ***I***nterface (API) is a very broad term where a software interacts with another piece of software. When people talk about API's, they usually talk about web API's. Some companies expose their endpoints, which will respond with code for consumers. It's like a portal into a different application. They occur over HTTP.

For example, on this website called [Cryptonator](https://www.cryptonator.com/api/), it gives us an endpoint for us to use, and it returns us JSON value

![img1](https://github.com/Brian-E-Nguyen/Web-Dev-Bootcamp-2020/blob/27-AJAX-and-APIs/27-AJAX-and-APIs/img-for-notes/img1.jpg?raw=true)

It's an interface not for humans, but rather web pages.

Some of them are free, some of them are not. It costs money for companies to receive requests

There are a bunch of different API's, like weather, Spotify song trends, Twitter etc. Long story short, there are many API's and we will be focusing on Web API's

## 3. WTF is JSON?

XML was once commonly used years ago, but now ***J***ava***S***cript ***O***bject ***N***otation (JSON) is being used more often than XML. Instead of AJAX, we use __AJAJ__. Whenever people say "AJAX", they most likely are referring to JSON now

```json
{
    "name": "Brian",
    "year": 2019,
    "hobbies": [
        ...
    ]
}
```

As you can see here, we have key-value pairs. All of the keys must be in double-quoted strings

JSON supports these values:
- object
- array
- string
- number
- "true"
- "false"
- "null"

Some values in JavaScript are not valid in JSON, like `undefined`.

### 3.1 Parsing and Working with JSON

Let's say we have a string of JSON data that we have retrieved somewhere

```js
//THIS IS A STRING OF JSON (NOT AN OBJECT)
const data = `{"ticker":{"base":"BTC","target":"USD","price":"11288.49813464","volume":"91769.69699773","change":"-46.29462447"},"timestamp":1596510482,"success":true,"error":""}`
```

In order to format this string into actual JSON object, we would need to do this:

```js
// THIS IS A JS OBJECT
const parsedData = JSON.parse(data);
```

### 3.2 Static Methods

`JSON.parse(text[, reviver])`

> Parses the string `text` as JSON

`JSON.stringify(value[, replacer[, space]])`

> Returns a JSON string corresponding to the specified value