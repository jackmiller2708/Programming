A greedy algorithm is an algorithmic [[Programming Paradigms|paradigm]] that follows the problem-solving heuristic of making the locally optimal choice at each stage with the hope of finding a global optimum. In other words, a greedy algorithm chooses the best possible option at each step, without considering the consequences of that choice on future steps.

The greedy algorithm is useful when a problem can be divided into smaller subproblems and the solution of each subproblem can be combined to solve the overall problem. The greedy algorithm can be used to solve optimization problems that involve finding the best solution among many possible solutions.

> [!warning]
> When the choice to apply the greedy method is made without conducting a thorough examination, the decision to utilize it can be somewhat difficult and occasionally even result in failure. In some cases taking the local best choice may lead to losing the global optimal solution.

It is important to prove the correctness of a greedy algorithm and to understand its limitations. The greedy algorithm can be applied in many contexts, including scheduling, graph theory, and [[Dynamic Programming|dynamic programming]].

> [!info]
> Greedy algorithm and Dynamic programming are two of the most widely used algorithm paradigms for solving complex programming problems, While Greedy approach works for problems where **local optimal** choice leads to global optimal solution Dynamic Programming works for problems having **[[Overlapping Subproblems|overlapping subproblems]]** structure where answer to a subproblem is needed for solving several other subproblems.

Greedy Algorithm is defined as a method for solving optimization problems by taking decisions that result in the most evident and immediate benefit irrespective of the final outcome. It works for cases where **minimization** or **maximization** leads to the required solution.

## Use Cases
- **Scheduling and Resource Allocation**: The greedy algorithm can be used to schedule jobs or allocate resources in an efficient manner.
- **Minimum Spanning Trees**: The greedy algorithm can be used to find the minimum spanning tree of a graph, which is the subgraph that connects all vertices with the minimum total edge weight.
- **Coin Change Problem**: The greedy algorithm can be used to make change for a given amount with the minimum number of coins, by always choosing the coin with the highest value that is less than the remaining amount to be changed.
- **Huffman Coding**: The greedy algorithm can be used to generate a prefix-free code for data compression, by constructing a binary tree in a way that the frequency of each character is taken into consideration.