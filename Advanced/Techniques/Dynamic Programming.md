Dynamic programming is a technique where an algorithmic problem is first broken down into sub-problems, the results are saved so the same problem will not have to be computed again, and then the sub-problems are optimized to find the overall solution — which usually has to do with finding the maximum and minimum range of the algorithmic query.  

## Characteristics of Dynamic Programming Algorithm
- The given problem can be broken up into smaller sub-problems, and these smaller subproblems can be divided into still smaller ones, and in this process, you see some overlapping subproblems.
- The solution to the problem can be constructed from the solutions to the subproblems.
- The optimal solutions to the subproblems contribute to the optimal solution of the given problem (referred to as the [[Optimal Structure|Optimal Substructure Property]]).
## Techniques to solve DP problems

1. Top-Down ([[Memoization]])
	-  Break down the given problem in order to begin solving it. If you see that the problem has already been solved, return the saved answer. If it hasn’t been solved, solve it and save it.
1. Bottom-Up ([[Tabulation]])
	- Analyze the problem and see in what order the subproblems are solved, and work your way up from the trivial subproblem to the given problem. This process ensures that the subproblems are solved before the main problem.
