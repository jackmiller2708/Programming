# Origin

Object-oriented programming, better known as OOP, is a programming paradigm that has become a fundamental aspect of modern software development. But did you know that OOP started as a programming blooper?

In the 1960s, computer scientists began working on a new programming language called Simula. The goal of Simula was to create a language that could simulate complex real-world systems, such as traffic flow or manufacturing processes.

To achieve this, the creators of Simula introduced the concept of "objects" - data structures that could contain both data and the functions that could operate on that data. The idea was to create a programming model that more closely resembled the real world, where objects interact with each other to achieve a specific goal.

Initially, this approach was seen as a blooper by many programmers. They felt that it was too complex and unnecessary, as traditional programming languages like FORTRAN and COBOL were already well-established and widely used.

However, as computer systems became more complex and the need for scalable and maintainable software increased, the benefits of OOP became clear. Today, OOP is the backbone of many popular programming languages, including Java, Python, and C++.

Undoubtedly, OOP is the dominant paradigm, but the argument is that most of its success is associated with languages that just happen to be OOP, and not because they were OOP.

# Caveat

OOP is considered by many to be the crown jewel of computer science. The ultimate solution to code organization. The end to all our problems. The only true way to write our programs. Bestowed upon us by the one true God of programming himself…

Until…it’s not, and people start succumbing under the weight of abstractions, and the complex graph of promiscuously shared mutable objects. Precious time and brainpower are being spent thinking about “abstractions” and “design patterns” instead of solving real-world problems.

Many people have criticized Object-Oriented Programming, including very prominent software engineers. Heck, even the inventor of OOP himself is a well-known critic of modern OOP!

The ultimate goal of every software developer should be to write reliable code. Nothing else matters if the code is buggy and unreliable. And what is the best way to write code that is reliable? Simplicity. Simplicity is the opposite of complexity. Therefore our first and foremost responsibility as software developers should be to reduce code complexity.

> Object oriented programs are offered as alternatives to correct ones… — _Edsger W. Dijkstra, pioneer of computer science._

The bitter truth is that OOP fails at the only task it was intended to address. It looks good on paper — we have clean hierarchies of animals, dogs, humans, etc. However, it falls flat once the complexity of the application starts increasing. Instead of reducing complexity, it encourages promiscuous sharing of mutable state and introduces additional complexity with its numerous design patterns. OOP makes common development practices, like refactoring and testing, needlessly hard.

Using OOP is seemingly innocent in the short-term, especially on greenfield projects. But what are the long-term consequences of using OOP? OOP is a time bomb, set to explode sometime in the future when the codebase gets big enough.

Projects get delayed, deadlines get missed, developers get burned-out, adding in new features becomes next to impossible. The organization labels the codebase as the “legacy codebase”, and the development team plans a rewrite.

OOP is not natural for the human brain, our thought process is centered around “doing” things — go for a walk, talk to a friend, eat pizza. Our brains have evolved to do things, not to organize the world into complex hierarchies of abstract objects.

OOP code is non-deterministic — unlike with functional programming, we’re not guaranteed to get the same output given the same inputs. This makes reasoning about the program very hard. As an oversimplified example, the output of `2+2` or `calculator.Add(2, 2)` mostly is equal to `4`, but sometimes it might become equal to `3`, `5`, and maybe even `1004`. The dependencies of the Calculator object might change the result of the computation in subtle, but profound ways.