We’ve been told that encapsulation is one of the greatest benefits of OOP. It is supposed to protect the object’s internal state from outside access. There’s a small problem with this though. It doesn’t work.

Encapsulation is the trojan horse of OOP. It sells the idea of shared mutable state by making it appear safe. Encapsulation allows (and even encourages) unsafe code to sneak into our codebase, making the codebase rot from within.

## **The global state problem**

We’ve been told that global state is the root of all evil. It should be avoided at all costs. What we have never been told is that encapsulation, in fact, is glorified global state.

To make the code more efficient, objects are passed not by their value, but by their reference. This is where “dependency injection” falls flat.

Let me explain. Whenever we create an object in OOP, we pass references to its dependencies to the constructor. Those dependencies also have their own internal state. The newly created object happily stores references to those dependencies in its internal state and is then happy to modify them in any way it pleases. And it also passes those references down to anything else it might end up using.

This creates a complex graph of promiscuously shared objects that all end up changing each other’s state. This, in turn, causes huge problems since it becomes almost impossible to see what caused the program state to change. Days might be wasted trying to debug such state changes. And you’re lucky if you don’t have to deal with concurrency.

## Methods/Properties

The methods or properties that provide access to particular fields are _no better_ than changing the value of a field directly. It doesn’t matter whether you mutate an object’s state by using a fancy property or method — the _result is the same: mutated state._