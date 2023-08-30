Alan Kay coined the term “Object Oriented Programming” in the 1960s. He had a background in biology and was attempting to make computer programs communicate the same way living cells do.

> I’m sorry that I long ago coined the term “objects” for this topic because it gets many people to focus on the lesser idea. The big idea is messaging. — _Alan Kay, the inventor of OOP_

His big idea was to have independent programs (cells) communicate by sending messages to each other. The state of the independent programs would never be shared with the outside world (encapsulation).

That’s it. OOP was never intended to have things like _inheritance_, _polymorphism_, _the “new” keyword_, and the myriad of design patterns.

The most important aspect of software development is keeping the code complexity down. Period. None of the fancy features matter if the codebase becomes impossible to maintain. Even 100% test coverage is worth nothing if the codebase becomes too complex and unmaintainable.

What makes the codebase complex? There are many things to consider, but in my opinion, the top offenders are: shared mutable state, erroneous abstractions, and low signal-to-noise ratio (often caused by boilerplate code). All of them are prevalent in OOP.