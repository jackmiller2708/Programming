What do we do when something is not working? It is simple, we only have two options — throw it away or try fixing it. OOP is something that can’t be thrown away easily, millions of developers are trained in OOP. And millions of organizations worldwide are using OOP.

You probably see now that OOP _doesn’t really work_, it makes our code complex and unreliable. And you’re not alone! People have been thinking hard for _decades_ trying to address the issues prevalent in OOP code. They’ve come up with a myriad of _design patterns_

## Design patterns

OOP provides a set of guidelines that should _theoretically_ allow developers to incrementally build larger and larger systems: SOLID principle, dependency injection, design patterns, and others.

Unfortunately, the design patterns are nothing other than band-aids. They exist solely to address the _shortcomings_ of OOP. A myriad of books has even been written on the topic. They wouldn’t have been so bad, had they not been responsible for the introduction of enormous complexity to our codebases.

## The problem factory

In fact, it is impossible to write good and maintainable Object-Oriented code.

On one side of the spectrum we have an OOP codebase that is inconsistent and doesn’t seem to adhere to any standards. On the other side of the spectrum, we have a tower of over-engineered code, a bunch of erroneous abstractions built one on top of one another. Design patterns are very helpful in building such towers of abstractions.

Soon, adding in new functionality, and even making sense of all the complexity, gets harder and harder. The codebase will be full of things like `SimpleBeanFactoryAwareAspectInstanceFactory`, `AbstractInterceptorDrivenBeanDefinitionDecorator`, `TransactionAwarePersistenceManagerFactoryProxy` or `RequestProcessorFactoryFactory` .

Precious brainpower has to be wasted trying to understand the tower of abstractions that the developers themselves have created. The absence of structure is in many cases better than having bad structure (if you ask me).