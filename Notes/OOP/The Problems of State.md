What is state? Simply put, state is any temporary data stored in memory. Think variables or fields/properties in OOP. Imperative programming (including OOP) describes computation in terms of the program state and changes to that state. Declarative (functional) programming describes the desired results instead, and don’t specify changes to the state explicitly.

## Mutable State

State by itself is quite harmless. However, mutable state is the big offender. Especially if it is shared. What exactly is mutable state? - Any state that can change. Think variables or fields in OOP.

> Real-world example, please!

You have a blank piece of paper, you write a note on it, and you end up with the same piece of paper in a different state (text). You, effectively, have mutated the state of that piece of paper.

That is completely fine in the real world since nobody else probably cares about that piece of paper. Unless this piece of paper is the original Mona Lisa painting.

### Limitations of the Human Brain

Why is mutable state such a big problem? The human brain is the most powerful machine in the known universe. However, our brains are really bad at working with state since we can only hold about 5 items at a time in our working memory. It is much easier to reason about a piece of code if you only think about what the code does, not what variables it changes around the codebase.

Programming with mutable state is an act of mental juggling️. I don’t know about you, but I could probably juggle two balls. Give me three or more balls and I will certainly drop all of them. Why are we then trying to perform this act of mental juggling every single day at work?

Unfortunately, the mental juggling of mutable state is at the very core of OOP. The sole purpose for the existence of methods on an object is to mutate that same object.

## **Scattered State**

OOP makes the problem of code organization even worse by scattering state all over the program. The scattered state is then shared promiscuously between various objects.

> Real-world example, please!

Let’s forget for a second that we’re all grown-ups, and pretend we’re trying to assemble a cool Lego truck.

However, there’s a catch — all the truck parts are randomly mixed with parts from your other Lego toys. And they have been put in 50 different boxes, randomly again. And you’re not allowed to group your truck parts together — you have to keep in your head where the various truck parts are, and can only take them out one by one.

Yes, you will eventually assemble that truck, but how long will it take you?

How does this relate to programming?

In Functional Programming, state typically is being isolated. You always know where some state is coming from. State is never scattered across your different functions. In OOP, every object has its own state, and when building a program , you have to keep in mind the state of all of the objects that you currently are working with.

To make our lives easier, it is best to have only a very small portion of the codebase deal with state. Let the core parts of your application be stateless and pure. This actually is the main reason for the huge success of the flux pattern on the frontend.

## **Promiscuously Shared State**

As if our lives aren’t already hard enough because of having scattered mutable state, OOP goes one step further!

> Real-world Example, Please!

Mutable state in the real world is almost never a problem, since things are kept private and never shared. This is “proper encapsulation” at work. Imagine a painter who is working on the next Mona Lisa painting. He is working on the painting alone, finishes up, and then sells his masterpiece for millions.

Now, he’s bored with all that money and decides to do things a little bit differently. He thinks that it would be a good idea to have a painting party. He invites his friends elf, Gandalf, policeman, and a zombie to help him out. Teamwork! They all start painting on the same canvas at the same time. Of course, nothing good comes out of it — the painting is a complete disaster!

Shared mutable state makes no sense in the real world. Yet this is exactly what happens in OOP programs — state is promiscuously shared between various objects, and they mutate it in any way they see fit. This, in turn, makes reasoning about the program harder and harder as the codebase keeps growing.

## **Concurrency issues**

The promiscuous sharing of mutable state in OOP code makes parallelizing such code almost impossible. Complex mechanisms have been invented in order to address this problem. Thread locking, mutex, and many other mechanisms. Of course, such complex approaches have their own drawbacks — deadlocks, lack of composability, debugging multi-threaded code is very hard and time-consuming. I’m not even talking about the increased complexity caused by making use of such concurrency mechanisms.

## **Not all state is evil**

Is all state evil? No, state probably is not evil! State mutation probably is fine if it is truly isolated (not the “OOP-way” isolated).

It is also completely fine to have immutable data-transfer-objects. The key here is “immutable”. Such objects are then used to pass data between functions.

However, such objects would also make OOP methods and properties completely redundant. What’s the use in having methods and properties on an object if it cannot be mutated?

## **Mutability is Inherent to OOP**

Some might argue that mutable state is a design choice in OOP, not an obligation. There is a problem with that statement. It is not a design choice, but pretty much the only option. Yes, one can pass immutable objects to methods in Java/C#, but this is rarely done since most of the developers default to data mutation. Even if developers attempt to make proper use of immutability in their OOP programs, the languages provide no built-in mechanisms for immutability, and for working effectively with immutable data (i.e. persistent data structures).

Yes, we can ensure that objects communicate only by passing immutable messages and never pass any references (which is rarely done). Such programs would be more reliable than mainstream OOP. However, the objects still have to mutate their own state once a message has been received. A message is a side effect, and its single purpose is to cause changes. Messages would be useless if they couldn’t mutate the state of other objects.

It is impossible to make use of OOP without causing state mutations.