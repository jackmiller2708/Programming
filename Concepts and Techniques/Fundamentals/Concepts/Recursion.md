The process in which a function calls itself **directly** or **indirectly** is called [[Recursion|recursion]] and the corresponding function is called a recursive function. Using a recursive algorithm, certain problems can be solved quite easily.  A recursive function solves a particular problem by calling a copy of itself and solving smaller subproblems of the original problems. In some cases, can be optimized by using [[Dynamic Programming|dynamic programming]] (DP).

It can reduce the length of our code and make it easier to read and write.

> [!warning]
> Recursion uses more memory, because the recursive function adds to the stack with each recursive call, and keeps the values there until the call is finished.

## Properties of Recursion
- Performing the same operations multiple times with different inputs.
- In every step, we try smaller inputs to make the problem smaller.
- Base condition is needed to stop the recursion otherwise infinite loop will occur.