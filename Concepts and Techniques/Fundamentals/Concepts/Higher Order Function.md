A **higher order function** (HOF) is a function that takes one or more functions as arguments, or returns a **function** as its result. As oppose to the **[[First-class Function|first-order functions]]** - the regular functions.

```js
// Callback function, passed as a parameter in the higher order function.
// This in and of itself is a first-order function.
function callbackFunction(){
    console.log('I am a callback function');
}

// Higher order function.
function higherOrderFunction(func){
    console.log('I am higher order function')
    func()
}

higherOrderFunction(callbackFunction);
```
Result:
```
I am higher order function
I am a callback function
```