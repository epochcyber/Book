# What is DOM-based XSS
DOM-based XSS Vulneability usually arises when Java-script take data from sourc and passes it to a sink that support dynamic code execution, such as eval() or innerHTML.

## Taint-flow vulnerabilities 
Taint-flow vulnerabilities occur when untrusted or potentially malicious input (referred to as “tainted data”) flows through an application without proper validation or sanitization, reaching a sensitive function or operation (referred to as a “sink”). This type of vulnerability can lead to various security issues, such as injection attacks (SQL injection, command injection, etc.), cross-site scripting (XSS), or even remote code execution (RCE), depending on how the tainted data is used.

## sources
A source in JavaScript is any location from which data is fetched or received that might be controlled by an external user or attacker. This untrusted data can be used in scripts or HTML without proper validation, leading to vulnerabilities like XSS.
```javascript
    document.URL
    document.documentURI
    document.URLUnencoded
    document.baseURI
    location
    document.cookie
    document.referrer
    window.name
    history.pushState
    history.replaceState
    localStorage
    sessionStorage
    IndexedDB (mozIndexedDB, webkitIndexedDB, msIndexedDB)
    Database
```
#### Sources example 

**example-1** --> user input field
```html
<input id="username" value="user_input"/>
<script>
  var userInput = document.getElementById('username').value; // Source: User input
</script>
```
**example-2** --> URL parameter 
```javascript
var urlParams = new URLSearchParams(window.location.search);
var param = urlParams.get('q'); // Source: URL parameter
```
**example-3** --> Cookies
```javascript
var cookieValue = document.cookie; // Source: Cookies
```
**example-4** --> Local Storage or Session Storage
```javascript
var storedData = localStorage.getItem('userData'); // Source: Local storage
```
**example-5** --> DOM
```javascript
var referrer = document.referrer; // Source: Referrer
```
**example-6** --> JavaScript Events
```javascript
var data = event.data; // Source: Data from JavaScript events
```

## Sink
A sink in JavaScript is any function or operation that uses untrusted data in a way that can affect the page’s structure, behavior, or security. This is where a security issue can occur if the tainted data (from the source) is not properly handled or sanitized before reaching the sink.

```Javascript
    document.write()
    window.location
    document.cookie
    eval()
    document.domain
    WebSocket()
    element.src
    postMessage()
    setRequestHeader()
    FileReader.readAsText()
    ExecuteSql()
    sessionStorage.setItem()
    document.evaluate()
    JSON.parse()
    element.setAttribute()
    RegExp()
```
#### Sink example

**example-1** DOM manipulation Functions
```Javascript
document.getElementById('output').innerHTML = userInput; // Sink: Modifying inner HTML

document.getElementById('element').outerHTML = userInput; // Sink: Modifying outer HTML

document.write(userInput); // Sink: Directly writing user-controlled data
```

**example-2** eval()
```Javascript
eval(userInput); // Sink: Executing user-controlled JavaScript

// setTimeout() and setInterval() (with string arguments):
setTimeout(userInput, 1000); // Sink: Executing user-controlled JavaScript after delay
```

**example-3** CSS injection 
```javascript
document.getElementById('style').innerHTML = userInput; // Sink: Injecting untrusted CSS
```

**example-4** Event Handler 
```javascript
var button = document.getElementById('btn');
button.setAttribute('onclick', userInput); // Sink: Setting an event handler to untrusted input
```

**example-5** iframe.src or img.src
```javascript
var iframe = document.createElement('iframe');
iframe.src = userInput; // Sink: Setting iframe source to untrusted input
document.body.appendChild(iframe);
```

**example-6** Function () Constructor 
```javascript
var func = new Function(userInput); // Sink: Creating a function with untrusted data
func();
```

**example-8** appendChild()
```javascript
var element = document.createElement('div');
element.innerHTML = userInput;
document.body.appendChild(element); // Sink: Appending untrusted content to the DOM
```


**Example of Source-to-Sink in JavaScript (XSS)**
```html
<input type="text" id="inputBox">
<div id="output"></div>

<script>
    // Source: User input from the text box
    var userInput = document.getElementById('inputBox').value;

    // Sink: Using the untrusted input in innerHTML without sanitization
    document.getElementById('output').innerHTML = userInput;
</script>
```