 Example 139. Word Break
Report Issue
In this article, we'll use the framework to solve Word Break. So far, in this card, this is the most unique and perhaps the most difficult problem to see that dynamic programming is a viable approach. This is because, unlike all of the previous problems, we will not be working with numbers at all. When a question asks, "is it possible to do..." it isn't necessarily a dead giveaway that it should be solved with DP. However, we can see that in this question, the order in which we choose words from \text{wordDict}wordDict is important, and a greedy strategy will not work.

Recall back in the first chapter, we said that a good way to check if a problem should be solved with DP or greedy is to first assume that it can be solved greedily, then try to think of a counterexample.

Let's say that we had \text{s} =s= "abcdef" and \text{wordDict = [}wordDict = [ "abcde", "ef", "abc", "a", "d"\text{]}]. A greedy algorithm (picking the longest substring available) will not be able to determine that picking "abcde" here is the wrong decision. Likewise, a greedy algorithm (picking the shortest substring available) will not be able to determine that picking "a" first is the wrong decision.

With that being said, let's develop a DP algorithm using our framework:

For this problem, we'll look at bottom-up first.

1. An array that answers the problem for a given state

Despite this problem being unlike the ones we have seen so far, we should still stick to the ideas of the framework. In the article where we learned about multi-dimensional dynamic programming, we talked about how an index variable, usually denoted \text{i}i is typically used in DP problems where the input is an array or string. All the problems that we have looked at up to this point reflect this.

With this in mind, let's use a state variable \text{i}i, which keeps track of which index we are currently at in \text{s}s.

Do we need any other state variables? The other input is \text{wordDict}wordDict - however, it says in the problem that we can reuse words from \text{wordDict}wordDict as much as we want. Therefore, a state variable isn't necessary because \text{wordDict}wordDict and what we can do with it never changes. If the problem was changed so that we can only use a word once, or say \text{k}k times, then we would need extra state variables to know what words we are allowed to use at each state.

In all the past problems, we had a function \text{dp}dp return the answer to the original problem for some state. We should try to do the same thing here. The problem is asking, is it possible to create \text{s}s by combining words in \text{wordDict}wordDict. So, let's have an array \text{dp}dp where \text{dp[i]}dp[i] represents if it is possible to build the string \text{s}s up to index \text{i}i from \text{wordDict}wordDict. To answer the original problem, we can return \text{dp[s.length - 1]}dp[s.length - 1] after populating \text{dp}dp.

2. A recurrence relation to transition between states

At each index \text{i}i, what criteria determines if \text{dp[i]}dp[i] is true? First, a word from \text{wordDict}wordDict needs to be able to end at index \text{i}i. In terms of code, this means that there is some \text{word}word from \text{wordDict}wordDict that matches the substring of \text{s}s that starts at index \text{i - word.length + 1}i - word.length + 1 and ends at index \text{i}i.

We can iterate through all states of \text{i}i from \text{0}0 up to but not including \text{s.length}s.length, and at each state, check all the words in \text{wordDict}wordDict for this criteria. For each \text{word}word in \text{wordDict}wordDict, if \text{s}s from index \text{i - word.length + 1}i - word.length + 1 to \text{i}i is equal to \text{word}word, that means \text{word}word ends at \text{i}i. However, this is not the sole criteria.

Remember, we are forming \text{s}s by adding words together. That means, if a \text{word}word meets the first criteria and we want to use it in a solution, we would add it on top of another string. We need to make sure that the string before it is also formable. If \text{word}word meets the first criteria, it starts at index \text{i - word.length + 1}i - word.length + 1. The index before that is \text{i - word.length}i - word.length, and the second criteria is that \text{s}s up to this index is also formable from \text{wordDict}wordDict. This gives us our recurrence relation:

dp(i) = true if s.substring(i - word.length + 1, i + 1) == word and dp[i - word.length] == true for any word in wordDict, otherwise false




In summary, the criteria is:

A \text{word}word from \text{wordDict}wordDict can end at the current index \text{i}i.

If that \text{word}word is to end at index \text{i}i, then it starts at index \text{i - word.length + 1}i - word.length + 1. The index before that \text{i - word.length}i - word.length should also be formable from \text{wordDict}wordDict.

3. Base cases

The base case for this problem is another simple one. The first word used from \text{wordDict}wordDict starts at index \text{0}0, which means we would need to check \text{dp[-1]}dp[-1] for the second criteria, which is out of bounds. To fix this, we say that the second criteria can also be satisfied by \text{i == word.length - 1}i == word.length - 1.



Bottom-up Implementation



Top-down Implementation
In the top-down approach, we can check for the base case by returning \text{true}true if \text{i < 0}i < 0. In Java, we will memoize by using a \text{-1}-1 to indicate that the state is unvisited, \text{0}0 to indicate \text{false}false, and \text{1}1 to indicate \text{true}true.


Let's say that \text{n = s.length}n = s.length, \text{k = wordDict.length}k = wordDict.length, and \text{L}L is the average length of the words in \text{wordDict}wordDict. While the space complexity for this problem is the same as the number of states \text{n}n, the time complexity is much worse. At each state \text{i}i, we iterate through \text{wordDict}wordDict and splice \text{s}s to a new string with average length \text{L}L. This gives us a time complexity of O(n \cdot k \cdot L)O(n⋅k⋅L).



Up Next
Before we move on to the next pattern, try the next practice problem which involves iteration on your own. It is a very classical computer science problem and is popular in interviews. As always, come back here if you need hints:

300. Longest Increasing Subsequence

Click here to show hint regarding state variables and dp
Let \text{dp[i]}dp[i] represent the length of the longest increasing subsequence that ends at index i.

Click here to show hint regarding recurrence relation
Let's say you have an index \text{j}j, where \text{j < i}j < i. If \text{nums[i] > nums[j]}nums[i] > nums[j], that means we can add onto whatever subsequence ends at index \text{j}j using \text{nums[i]}nums[i].

Click here to show hint regarding base cases
By default, every number on its own is an increasing subsequence of length 1.

