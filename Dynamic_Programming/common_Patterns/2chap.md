Example 1335. Minimum Difficulty of a Job Schedule
Report Issue
We'll start with a top-down approach.

In this article, we'll be using the framework to solve Minimum Difficulty of a Job Schedule. We can tell this is a problem where Dynamic Programming can be used because we are asked for the minimum of something, and deciding how many jobs to do on a given day affects the jobs we can do on all future days. Let's start solving:

1. A function that answers the problem for a given state

Let's first decide on state variables. What decisions are there to make, and what information do we need to make these decisions? Reading the problem description carefully, there are \text{d}d total days, and on each day we need to complete some number of jobs. By the end of the \text{d}d days, we must have finished all jobs (in the given order). Therefore, we can see that on each day, we need to decide how many jobs to take.

Let's use one state variable \text{i}i, where \text{i}i is the index of the first job that will be done on the current day.

Let's use another state variable \text{day}day, where \text{day}day indicates what day it currently is.

The problem is asking for the minimum difficulty, so let's have a function \text{dp(i, day)}dp(i, day) that returns the minimum difficulty of a job schedule which starts on the i^{th}i 
th
  job and day, \text{day}day. To solve the original problem, we will just return \text{dp(0, 1)}dp(0, 1), since we start on the first day with no jobs done yet.



2. A recurrence relation to transition between states

At each state, we are on day \text{day}day and need to do job \text{i}i. Then, we can choose to do a few more jobs. How many more jobs are we allowed to do? The problem says that we need to do at least one job per day. This means we must leave at least \text{d - day}d - day jobs so that all the future days have at least one job that can be scheduled on that day. If \text{n}n is the total number of jobs, \text{jobDifficulty.length}jobDifficulty.length, that means from any given state \text{(i, day)}(i, day), we are allowed to do the jobs from index \text{i}i up to but not including index \text{n - (d - day)}n - (d - day).

We should try all the options for a given day - try doing only one job, then two jobs, etc. until we can't do any more jobs. The best option is the one that results in the easiest job schedule.

The difficulty of a given day is the most difficult job that we did that day. Since the jobs have to be done in order, if we are trying all the jobs we are allowed to do on that day (iterating through them), then we can use a variable \text{hardest}hardest to keep track of the difficulty of the hardest job done today. If we choose to do jobs up to the j^{th}j 
th
  job (inclusive), where \text{i} \leq \text{j} < \text{n - (d - day)}i≤j<n - (d - day) (as derived above), then that means on the next day, we start with the (j + 1)^{th}(j+1) 
th
  job. Therefore, our total difficulty is \text{hardest + dp(j + 1, day + 1)}hardest + dp(j + 1, day + 1). This gives us our scariest recurrence relation so far:

\text{dp(i, day) = min(hardest + dp(j + 1, day + 1))}dp(i, day) = min(hardest + dp(j + 1, day + 1)) for all \text{i} \leq \text{j} < \text{n - (d - day)}i≤j<n - (d - day), where \text{hardest = max(jobDifficulty[k])}hardest = max(jobDifficulty[k]) for all \text{i} \leq \text{k} \leq \text{j}i≤k≤j.

The codified recurrence relation is a scary one to look at for sure. However, it is easier to understand when we break it down bit by bit. On each day, we try all the options - do only one job, then two jobs, etc. until we can't do any more (since we need to leave some jobs for future days). \text{hardest}hardest is the hardest job we do on the current day, which means it is also the difficulty of the current day. We add \text{hardest}hardest to the next state which is the next day, starting with the next job. After trying all the jobs we are allowed to do, choose the best result.

Current
1 / 3


3. Base cases

Despite the recurrence relation being complicated, the base cases are much simpler. We need to finish all jobs in \text{d}d days. Therefore, if it is the last day (\text{day == d}day == d), we need to finish up all the remaining jobs on this day, and the total difficulty will just be the largest number in \text{jobDifficulty}jobDifficulty on or after index \text{i}i.

\text{if day == d}if day == d then return the maximum job difficulty between job \text{i}i and the end of the array (inclusive).

We can precompute an array \text{hardestJobRemaining}hardestJobRemaining where \text{hardestJobRemaining[i]}hardestJobRemaining[i] represents the difficulty of the hardest job on or after day \text{i}i, so that we this base case is handled in constant time.

Additionally, if there are more days than jobs (\text{n < d}n < d), then it is impossible to do at least one job each day, and per the problem description, we should return \text{-1}-1. We can check for this case at the very start.



Top-down Implementation
Let's combine these 3 parts for a top-down implementation. Again, we will use functools in Python, and a 2D array in Java for memoization. In the Python implementation, we are passing \text{None}None to lru_cache which means the cache size is not limited. We are doing this because the number of states that will be re-used in this problem is large, and we don't want to evict a state early and have to re-calculate it.




Bottom-up Implementation
With bottom-up, we now use a 2D array where \text{dp[i][day]}dp[i][day] represents the minimum difficulty of a job schedule that starts on day \text{day}day and job \text{i}i. It depends on the problem, but the bottom-up code generally has a faster runtime than its top-down equivalent. However, as you can see from the code, it looks like it is more challenging to implement. We need to first tabulate the base case and then work backwards from them using nested for loops.

The for-loops should start iterating from the base cases, and there should be one for-loop for each state variable. Remember that one of our base cases is that on the final day, we need to complete all jobs. Therefore, our for-loop iterating over \text{day}day should iterate from the final day to the first day. Then, our next for-loop for \text{i}i should conform to the restraints of the problem - we need to do at least one job per day.


Here's an animation showing the algorithm in action:

Current
1 / 30


The time and space complexity of these algorithms can be quite tricky, and as in this example, there are sometimes slight differences between the top-down and bottom-up complexities.

Let's start with the bottom-up space complexity, because it follows what we learned in the previous chapter about finding time and space complexity. For this problem, the number of states is n \cdot dn⋅d. This means the space complexity is O(n \cdot d)O(n⋅d) as our \text{dp}dp table takes up that much space.

The top-down algorithm's space complexity is actually a bit better. In top-down, when we memoize results with a hashtable, the hashtable's size only grows when we visit a state and calculate the answer for it. Because of the restriction of needing to complete at least one task per day, we don't actually need to visit all n \cdot dn⋅d states. For example, if there were \text{10}10 jobs and \text{5}5 days, then the state \text{(9, 2)}(9, 2) (starting the final job on the second day) is not reachable, because the 3rd, 4th, and 5th days wouldn't have a job to complete. This is true for both implementations and is enforced by our for-loops, and as a result, we only actually visit d \cdot (n - d)d⋅(n−d) states. This means the space complexity for top-down is O(d \cdot (n - d))O(d⋅(n−d)). This is one advantage that top-down can have over bottom-up. With the bottom-up implementation, we can't really avoid allocating space for n \cdot dn⋅d states because we are using a 2D array.

The time complexity for both algorithms is more complicated. As we just found out, we only actually visit d \cdot (n - d)d⋅(n−d) states. At each state, we go through a for-loop (with variable \text{j}j) that iterates on average \dfrac{n - d}{2} 
2
n−d
​	
  times. This means our time complexity for both algorithms is O(d \cdot (n - d)^2)O(d⋅(n−d) 
2
 ).

To summarize:

Time complexity (both algorithms): O(d \cdot (n - d)^2)O(d⋅(n−d) 
2
 )

Space complexity (top-down): O((n - d) \cdot d)O((n−d)⋅d)

Space complexity (bottom-up): O(n \cdot d)O(n⋅d)

While the theoretical space complexity is better with top-down, practically speaking, the 2D array is more space-efficient than a hashmap, and the difference in space complexities here doesn't justify saying that top-down will use less space than bottom-up.



Up Next
The next problem is a classical one and popular in interviews. Try it out yourself, and come back here if you need some hints:

322. Coin Change

Click here to show hint regarding state variables and \text{dp}dp
Let \text{dp[i]}dp[i] represent the fewest number of coins needed to make up \text{i}i money.

Click here to show hint regarding the recurrence relation.
For each coin available, we can get to \text{i}i from \text{i - coin}i - coin. Make sure that \text{coin} \leq \text{i}coin≤i.

Click here to show hint regarding the base cases.
According to the constraints, the minimum value for a coin is 1. Therefore, it is impossible to have 0 money, therefore \text{dp[0] = 0}dp[0] = 0.

