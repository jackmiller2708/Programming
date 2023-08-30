Automated testing is an important part of the development process and helps tremendously in preventing regressions (i.e. bugs being introduced into existing code). _Unit Testing_ plays a huge role in the process of automated testing.

Some might disagree, but OOP code is notoriously difficult to unit test. Unit Testing assumes testing things in isolation, and to make a method unit-testable:

1. Its dependencies have to be extracted into a separate class.
2. Create an interface for the newly created class.
3. Declare fields to hold the instance of the newly created class.
4. Make use of a mocking framework to mock the dependencies.
5. Make use of a dependency-injection framework to inject the dependencies.

How much more complexity has to be created just to make a piece of code testable? How much time was wasted just to make some code testable?

> PS: we’d also have to instantiate the entire class in order to test a single method. This will also bring in the code from all of its parent classes.

With OOP, writing tests for legacy code is even harder — almost impossible. Entire companies have been created around the issue of testing legacy OOP code.

## Testing private methods

Some people say that private methods shouldn’t be tested… I tend to disagree, unit testing is called “unit” for a reason — test small units of code in isolation. Yet testing of private methods in OOP is nearly impossible. We shouldn’t be making private methods `internal` just for the sake of testability.

In order to achieve testability of private methods, they usually have to be extracted into a separate object. This, in turn, introduces unnecessary complexity and [[Boilerplate code|boilerplate code]].