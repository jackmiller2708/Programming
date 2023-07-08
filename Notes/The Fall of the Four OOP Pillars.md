The four pillars of OOP are: Abstraction, Inheritance, Encapsulation, and Polymorphism. Let’s see what they really are, one-by-one.

## Inheritance

> I think the lack of reusability comes in object-oriented languages, not in functional languages. Because the problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.
> 
> — Joe Armstrong, creator of Erlang

OOP inheritance has nothing to do with the real world. Inheritance, in fact, is an inferior way to achieve code reusability. The gang of four has explicitly recommended preferring composition over inheritance. Some modern programming languages avoid inheritance altogether.

There are a few problems with inheritance:

1. Bringing in a lot of code that your class doesn’t even need (banana and the jungle problem).
2. Having parts of your class defined somewhere else makes the code hard to reason about, especially with multiple levels of inheritance.
3. In most programming languages, multiple inheritance isn’t even possible. This mostly renders inheritance useless as a code-sharing mechanism.

## OOP polymorphism

Polymorphism is great, it allows us to change program behavior at runtime. However, it is a very basic concept in computer programming. I’m not too sure why OOP focuses so much on polymorphism. OOP polymorphism gets the job done but once again it results in the act of mental juggling. It makes the codebase significantly more complex, and reasoning about the concrete method that is being invoked becomes really hard.

Functional programming, on the other hand, allows us to achieve the same polymorphism in a much more elegant way…by simply passing in a function that defines the desired runtime behavior. What could be simpler than that? No need to define a bunch of overloaded abstract virtual methods in multiple files (and the interface).

## Encapsulation

As we discussed earlier, encapsulation is [[The Trojan Horse of Encapsulation|the trojan horse of OOP]]. It is actually a glorified global mutable state and makes the _unsafe_ code appear safe. An unsafe coding practice is a pillar that OOP programmers rely on in their day-to-day job…

## Abstraction

Abstraction in OOP attempts to tackle complexity by hiding unnecessary details from the programmer. _Theoretically_, it should allow the developer to reason about the codebase without having to think about the hidden complexity.

I don’t even know what to say…a fancy word for a simple concept. In procedural/functional languages we can simply “hide” the implementation details in a neighboring file. No need to call this basic act an “abstraction”.