**Memoization is an optimization technique** that makes applications more efficient and hence faster. It does this by storing computation results in cache, and retrieving that same information from the cache the next time it's needed instead of computing it again.

In simpler words, it consists of storing in **cache** the output of a function, and making the function check if each required computation is in the cache before computing it. 

## In the context of Dynamic Programming
Memoization is a **top-down** approach where we cache the results of function calls and return the cached result if the function is called again with the same inputs. Memoization is typically implemented using [[Recursion|recursion]] and is well-suited for problems that have a relatively small set of inputs.