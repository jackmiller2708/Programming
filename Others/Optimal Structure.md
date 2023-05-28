A problem is said to have **optimal substructure** if an optimal solution can be constructed from optimal solutions of its subproblems. This property is used to determine the usefulness of [[Greedy Algorithm|greedy algorithms]] for a problem.

Typically, a greedy algorithm is used to solve a problem with optimal substructure if it can be proven by induction that this is optimal at each step. Otherwise, provided the problem exhibits **overlapping subproblems** as well, divide-and-conquer methods or [[Dynamic Programming|dynamic programming]] may be used. 

If there are no appropriate greedy algorithms and the problem fails to exhibit overlapping subproblems, often a lengthy but straightforward search of the solution space is the best alternative.