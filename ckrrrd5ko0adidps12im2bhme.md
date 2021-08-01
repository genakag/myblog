## The weird quirk of console.log in browsers

# The weird quirk of console.log in browsers

## The goal of this post
I want to clarify what happens with console.log on certain conditions so that I can log in my intended way.

## TLDR
When logging objects with `console.log`, clone them first before logging.
```javascript
var obj = { value: "hello" };

var objClone = JSON.parse(JSON.stringify(obj));
console.log(objClone);
```

## The weird quirk
When logging objects with `console.log`, the browser does not show the value at the time it was logged. The browser actually shows the value at the time the log was expanded. 

To show this quirk, I executed some commands on the chrome browser. I also took a screenshot of that to make it easier to understand what is happening. 

```javascript
var obj = { value: "hello" }
console.log(obj) // expanded right after execution
console.log(obj) // expanded after executing the code below
obj.value = "world"
```

![logging-screenshot.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627733964148/1lhsBDL7t.png)

You can see in the screenshot that although `console.log` is executed twice in a row, different results are showing.

## Logging the value at the time `console.log` was called
When using `console.log`, I usually want it to log the value at the time of logging. I was able to do this by cloning the object I want to clone just before logging. 

```javascript
var obj = { value: "hello" };

var objClone = JSON.parse(JSON.stringify(obj));
console.log(objClone);
```

Now I usually wrap the object with `JSON.parse` and `JSON.stringify` whenever I log for debugging. I also like to make my own function so that I don't have to worry about cloning every time I log.

```javascript
function log(obj) {
  console.log(JSON.parse(JSON.stringify(obj)));
}
```

## Thanks!
Thank you for reading till the end!

I would be happy to see some feedback, so please let me know your thoughts!