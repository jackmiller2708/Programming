What is a monad? Perhaps the most intuitive way to think about monads is as **chainable computations**, or even “programmable semicolons.” They allow us to wrap up computations and sequence them in meaningful ways.

A monad must have three particular properties and obey three particular laws. Of the three properties it must:
- Have a _type constructor_ that defines its type.
- Have a _unit function_ that converts a value of some type to its corresponding monadic type. 
- Have a _binding operation_ that takes a monad, a function that takes a some type and returns a monad. 

As for the three laws, these are known as: _left identity_, _right identity_, and _associativity_.
### Left Identity
```JS
M(x).bind(fn) == M(fn(x)); // for all x, fn
```
### Right Identity
```JS
M(x).bind(function(x){return x;}) == M(x); // for all x
```
### Associativity
```JS
M(x).bind(fn).bind(gn) == M(x).bind(function(x) {
  return gn(fn(x));
}); // for all x, fn, gn
```