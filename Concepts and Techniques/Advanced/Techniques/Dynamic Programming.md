**Dynamic programming** (DP) is a technique where an algorithmic problem is first broken down into subproblems, the results are saved so the same problem will not have to be computed again, and then the subproblems are optimized to find the overall solution — which usually has to do with finding the **maximum** and **minimum** range of the algorithmic query, so simply, it requires the use of previous states. 

## Characteristics of DP problems
- The given problem can be broken up into smaller subproblems, and these smaller subproblems can be divided into still smaller ones, and in this process, you see some [[Overlapping Subproblems|overlapping subproblems]].
- The solution to the problem can be constructed from the solutions to the subproblems.
- The optimal solutions to the subproblems contribute to the optimal solution of the given problem (referred to as the [[Optimal Structure|Optimal Substructure Property]]).
## Techniques to solve DP problems

1. Top-Down ([[Memoization]])
	-  Break down the given problem in order to begin solving it. If you see that the problem has already been solved, return the saved answer. If it hasn’t been solved, solve it and save it.
2. Bottom-Up ([[Tabulation]])
	- Analyze the problem and see in what order the subproblems are solved, and work your way up from the trivial subproblem to the given problem. This process ensures that the subproblems are solved before the main problem.

## Steps to solve DP problems
1. Identify if it is a DP problem.
2. Decide a state expression with the Least parameters.
3. Formulate state and transition relationship.
4. Do tabulation (or memorization).

### Step 1: Classifying the problem
Typically, all the problems - that require **maximizing or minimizing** certain quantities or counting problems that say to count the arrangements under certain conditions or certain probability -  can be solved by using DP.

All DP problems satisfy 
1. the <u>**overlapping subproblems**</u> property and 
2. most of the classic DP problems also satisfy the <u>**optimal substructure**</u> property. 

Once we've observed these properties in a given problem be sure that it can be solved using Dynamic Programming.

### Step 2: Deciding the state
DP problems are all about the **state** and its **transition**. This is the most basic step which must be done very carefully because the state transition depends on the choice of state definition you make.
>[!info]
>A **state** can be defined as the set of **parameters** that can uniquely identify a certain position or standing in the given problem. This set of parameters should be as small as possible to reduce state space.

For example, in the famous **Knapsack problem**, 
> We are given `N` items where each item has some `weight` and `profit` associated with it. We are also given a bag with capacity `W` - i.e. the bag can hold at most `W weight` in it). The target is to put the items into the bag such that the sum of profits associated with them is the maximum possible. 
> 
> **Note:** The constraint here is we can either put an item completely into the bag or cannot put it at all - _It is not possible to put a part of an item into the bag_.
> 
> **Example**:
> - **Input**: `W = 4, N = 3, profit = [1, 2, 3], weight = [4, 5, 1]`
> - **Output**: `3`
> - **Explanation:** There are two items which have weight less than or equal to `4`. If we select the item with weight `4`, the possible profit is `1`. And if we select the item with weight `1`, the possible profit is `3`. So the maximum possible profit is `3`. Note that we cannot put both the items with weight `4` and `1` together as the capacity of the bag is `4`.

A simple solution is to consider all subsets of items and calculate the total weight and profit of all subsets. Consider the only the subsets whose total weight is smaller than `W`. From all such subsets, pick the subset with maximum profit.

_**Optimal Substructure**_**:** To consider all subsets of items, there can be two cases for every item. 
- **Case 1:** The item is included in the optimal subset.
- **Case 2:** The item is not included in the optimal subset.

we define our state by two parameters `index` and `weight` - i.e. `DP[index][weight]`. 

Here `DP[index][weight]` tells us the maximum profit it can make by taking items from range `1` to `index` having the capacity of sack from range `1` to `W` to be `weight`. Therefore, here the parameters `index` and `weight` together can uniquely identify a subproblem for the Knapsack problem.

### Step 3: Formulating a relation among states
This part is the _hardest_ part of solving a DP problem and requires a lot of intuition, observation, and **PRACTICE!!**
#### How to compute state?
Let us go back the the Knapsack problem's state. 

The state `DP[index][weight]` will denote the maximum of  the bag's `weight` capacity considering all values from `1` to `index`. So if we consider the `weight` of item at `index` we can fill it in <u>**ALL**</u> columns which have the bag's `weight` capacity > item's `weight`.  

> [!note]
> Let's denote
> - `i` as value of the `index`
> - `j` as value from `0` to `W` 
> - `wi` as value of item's weight at `index`
> - `pi` as value of item's profit at `index`

Below is an illustration of how the states would look like:

| i / j | 0 | 1 | ... | W |
|-------| - | - | --- | - |
| 0     |   |   |     |   |
| 1     |   |   |     |   |
| ...   |   |   |     |   |
| N     |   |   |     |   |

Now two possibilities can take place for each `j` up to `W`:
- **Case 1**: Fill the element in the given `j`.
- **Case 2**: Do not fill the element in the given `j`.

Then, we have to take a maximum of these two possibilities, respectively,
- **Case 1**: if we fill the element in the given `j` => `DP[i][j] = sum(pi, DP[i - 1][j - wi])` .
- **Case 2**: if we do not fill the element in the given `j` => `DP[i][j] = DP[i - 1][j]` .

finally, we take the maximum of these two possibilities to fill the current state.

#### Illustration
> Let, `weight = [1, 2, 3]`, `profit = [10, 15, 40]`, `W = 6`.

For filling the first item in the bag:  `i = 1`, `wi = 1` and `pi = 10`
- when `j = 0`, then at this capacity, the bag cannot hold any item so the maximum `pi = 0` 
- when `j = 1`, then the maximum profit can be `max(DP[1][1], sum(10, DP[0][0])) = 10`

| i / j | 0 | 1  | 2  | 3  | 4  | 5  | 6  |
|-------| - | -- | -- | -- | -- | -- | -- |
| 0     | 0 | 0  | 0  | 0  | 0  | 0  | 0  |
| 1     | 0 | 10 | 10 | 10 | 10 | 10 | 10 |
| 2     |   |    |    |    |    |    |    |
| 3     |   |    |    |    |    |    |    |

For filling the second item in the bag: `i = 2`, `wi = 2`, `pi = 15`
- when `j = 1`, then maximum possible profit is `DP[1][1] = 10` as we cannot put the element.
- when `j = 2`, then maximum possible profit is `max(DP[1][2], sum(DP[1][0], 15)) = 15`.
- when `j = 3`, then maximum possible profit is `max(DP[1][3], sum(DP[1][1], 15)) = 25`.

| i / j | 0 | 1  | 2  | 3  | 4  | 5  | 6  |
|-------| - | -- | -- | -- | -- | -- | -- |
| 0     | 0 | 0  | 0  | 0  | 0  | 0  | 0  |
| 1     | 0 | 10 | 10 | 10 | 10 | 10 | 10 |
| 2     | 0 | 10 | 15 | 25 | 25 | 25 | 25 |
| 3     |   |    |    |    |    |    |    |

For filling the third item in the bag: `i = 3` and `wi = 3`, `pi = 40`
- when `j = 2`, then maximum possible profit is `DP[2][2] = 15` as we cannot put the element
- when `j = 3`, then maximum possible profit is `max(DP[2][3], sum(DP[2][0], 40)) = 40`.
- when `j = 4`, then maximum possible profit is `max(DP[2][4], sum(DP[2][1], 40)) = 50`.
- when `j = 5`, then maximum possible profit is `max(DP[2][5], sum(DP[2][2], 40)) = 55`.
- when `j = 6`, then maximum possible profit is `max(DP[2][6], sum(DP[2][3], 40)) = 65`.

| i / j | 0 | 1  | 2  | 3  | 4  | 5  | 6  |
|-------| - | -- | -- | -- | -- | -- | -- |
| 0     | 0 | 0  | 0  | 0  | 0  | 0  | 0  |
| 1     | 0 | 10 | 10 | 10 | 10 | 10 | 10 |
| 2     | 0 | 10 | 15 | 25 | 25 | 25 | 25 |
| 3     | 0 | 10 | 15 | 40 | 50 | 55 | 65 |

### Step 4: Adding memoization or tabulation for the state

This is the easiest part of a DP solution.

#### Memoization

As can be seen from Step 3, there are repetitions of the same subproblem again and again we can implement the following idea to solve the problem.

> If we get a subproblem the first time, we can solve this problem by creating a 2-D array that can store a particular state(n, w). Now if we come across the same state(n, w) again instead of calculating it in exponential complexity we can directly return its result stored in the table in constant time.

```JS 
function knapSack(W, index, weight, profit, dp = undefined) {
  // Creates a 2D array to store the value should there is not already one.
  // We plus one as the base case to be no item to be put in no bag where profit would be 0.
  const _dp = dp ?? new Array(N + 1).fill(-1).map(() => new Array(W + 1).fill(-1));

  // Base case
  if (index == 0 || W == 0) {
    return 0;
  }

  // Return the calculated result
  if (_dp[index][W] != -1) {
    return _dp[index][W];
  }

  // Current Item's index counting from base case as 0
  // where there is no element to be put in the bag
  // and the first element - the real element - would be at index 1
  const prevIndex = index - 1;

  // current Item's values
  const currWeight = weight[prevIndex];
  const currProfit = profit[prevIndex];

  // Case when weight is filled in the column.
  const fillVal = currProfit + knapSack(W - currWeight, prevIndex, weight, profit, _dp);

  // Case when weight is not filled in the column. Get the previous calculated profit.
  const doNotFillVal = knapSack(W, prevIndex, weight, profit, _dp);

  // Return value of table after storing
  return (_dp[index][W] = Math.max(doNotFillVal, fillVal));
}
```

**Time Complexity:** `O(N * W)`. As redundant calculations of states are avoided.  
**Auxiliary Space:** `O(N * W) + O(N)`. The use of a 2D array data structure for storing intermediate states and `O(N)` auxiliary stack space (ASS) has been used for recursion stack.

#### Tabulation

We implement the same logic but instead of recursion, we use iteration.

```JS
function knapSack(W, weightArr, profitArr, N) {
  // Making and initializing dp array
  var dp = Array(W + 1).fill(0);

  for (let index = 1; index < N + 1; index++) {
	const prevIndex = index - 1;
	const currProfit = profitArr[prevIndex];
    const currWeight = weightArr[prevIndex];
    
    for (let weight = W; weight >= 0; weight--) {
      if (currWeight <= weight) {
        const doNotFillVal = dp[weight];
        const fillVal = dp[weight - currWeight] + currProfit;

        // Finding the maximum value
        dp[weight] = Math.max(fillVal, doNotFillVal);
      }
    }
  }

  // Returning the maximum value of knapsack
  return dp[W];
}
```

**Time Complexity:**` O(N * W)`. where `N` is the number of elements and `W` is capacity.   
**Auxiliary Space:** `O(W)` As we are using a 1D array instead of a 2D array