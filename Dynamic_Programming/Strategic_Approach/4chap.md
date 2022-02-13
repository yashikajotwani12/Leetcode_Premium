Top-down to Bottom-up
Report Issue
As we've said in the previous chapter, usually a top-down algorithm is easier to implement than the equivalent bottom-up algorithm. With that being said, it is useful to know how to take a completed top-down algorithm and convert it to bottom-up. There's a number of reasons for this: first, in an interview, if you solve a problem with top-down, you may be asked to rewrite your solution in an iterative manner (using bottom-up) instead. Second, as we mentioned before, bottom-up usually is more efficient than top-down in terms of runtime.

Steps to convert top-down into bottom-up

Start with a completed top-down implementation.

Initialize an array \text{dp}dp that is sized according to your state variables. For example, let's say the input to the problem was an array \text{nums}nums and an integer \text{k}k that represents the maximum number of actions allowed. Your array \text{dp}dp would be 2D with one dimension of length \text{nums.length}nums.length and the other of length \text{k}k. The values should be initialized as some default value opposite of what the problem is asking for. For example, if the problem is asking for the maximum of something, set the values to negative infinity. If it is asking for the minimum of something, set the values to infinity.

Set your base cases, same as the ones you are using in your top-down function. Recall in House Robber, \text{dp(0) = nums[0]}dp(0) = nums[0] and \text{dp(1) = max(nums[0], nums[1])}dp(1) = max(nums[0], nums[1]). In bottom-up, \text{dp[0] = nums[0]}dp[0] = nums[0] and \text{dp[1] = max(nums[0], nums[1])}dp[1] = max(nums[0], nums[1]).

Write a for-loop(s) that iterate over your state variables. If you have multiple state variables, you will need nested for-loops. These loops should start iterating from the base cases.

Now, each iteration of the inner-most loop represents a given state, and is equivalent to a function call to the same state in top-down. Copy the logic from your function into the for-loop and change the function calls to accessing your array. All \text{dp(...)}dp(...) changes into \text{dp[...]}dp[...].

We're done! \text{dp}dp is now an array populated with the answer to the original problem for all possible states. Return the answer to the original problem, by changing \text{return dp(...)}return dp(...) to \text{return dp[...]}return dp[...].

Let's try a quick example using the House Robber code from before. Here's a completed top-down solution:


First, we initialize an array \text{dp}dp sized according to our state variables. Our only state variable is \text{i}i which can take \text{n}n values.


Second, we should set our base cases. \text{dp[0] = nums[0]}dp[0] = nums[0] and \text{dp[1] = max(nums[0], nums[1])}dp[1] = max(nums[0], nums[1]). To avoid index out of bounds, we should also just return \text{nums[0]}nums[0] if theres only one house.


Next, write a for-loop to iterate over the state variables, starting from the base cases.


Lastly, copy the recurrence relation over from the top-down solution and put it in the for-loop. Return \text{dp[n - 1]}dp[n - 1].

