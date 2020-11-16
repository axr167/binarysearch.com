# Problems

### Question 340: Run length Decoding

Characters can be double digit; Remember to use functions like `Character.isDigit` and `Character.getNumericValue` to append to stringbuilder

--------------

### Question 267: Number of Hops
Dp problem. Set min to max int, careful about overflow when a[i] = 0.
```
dp[i] = 0 // if i = a.length
dp[i] = 1 + min(dp[i+1] ... dp[i+a[i]]) // otherwise
```

-------------

### Question 40: Reverse a Linked List
To do it in O(1) space allocate a new head node at start of the list and make `head.next = node`. While `node.next != null`, make `node.next` the next of head. Return `head.next`

-------------

### Question 4: Hoppable
Greedy problem. Loop through all elements of list and maintain max hop length `max`. Update max as `max = max(max, i+nums[i])`. If `max >= len` return true. If `max = i` return false.

------------

### Question 118: Space Battle
Monotonic Queue. Iterate over all elements. Have a boolean variable `canAdd` set to true. While queue is not empty && first element is positive && a[i] is negative, begin loop of destruction. In loop of destruction: 
    
- if abs of a[i] is more than first element, remove element. 
- Otherwise if they are equal, remove first element, make `canAdd = false` and break. 
- Otherwise if abs of a[i] smaller than first element, break
 
If we can still add, add a[i] to front of queue. When we have finished iteration, empty queue into result array.

------------

### Question 736: Longest Equivalent Sublist After K Increments
Here we need to find the longest sliding window where we can make all elements equal by incrementing values at most k times.

Number of increments in sliding window requires us to find largest element in sliding window. To find largest element in a sliding window use Monotonic Queue.

- Start with `l = 0` - this is left pointer. Then iterate through the list here `i` is the right pointer
- An increasing a monotonic queue keeps track of largest element between `l...i`. We also maintain a running sum so for each `i`, do `runningSum += nums[i]`
- The required sum to make everything = the largest element is width * max element in window ie `(i-l+1) * deque.peekLast()`
    - If this value is less than k, then `maxWindow = max(maxWindow, i-l+1)`
    - Otherwise while the value is greater than k do the following in a loop:
        - increment l. If the last element in deque was nums[l] it should be removed. also decrement nums[l] from running sum
        - get new value by doing `(i-l+1) * deque.peekLast()`

-------------

### Question 20: Subsequence Strings
DP problem. O(n^2) time and O(n) space. Recurrence is below:

```
f(i, j) = true if i = s1.length
f(i, j) = false if j = s2.length
f(i, j) = f(i+1, j+1) if s1[i] = s2[j]
f(i, j) = f(i, j+1) if s1[i] != s2[j]
```

------------

### Question 83: Most Frequent Subtree Sum
Do postorder traversal storing sum, count in hashmap. Keep track of maxCount and maxKey in global variables and update them as we do the traversal. In the end return the maxKey.

----------

### Question 814: Removing Triple Successive Duplicates
2 pointer method. Look for substrings that have same-digit and divide by 3. Intuition is that if we have N of the same characters, it takes `N/3` operations to make sure no 3 characters are same.

------

### Question 45: Golden Gate Bridge
BFS problem where we treat any node that forms edge of island 1 as a possible start point and any node that forms an edge of island 2 as a possible end point. 
Declare the following: 1) A dist matrix to keep track of visited cells + the distances 2) Row queue and Column queue for bfs. Then do the following:

- Iterate over matrix to find first island. We do this by looking for the first '1' once we have done that do a dfs to mark the island.
  - In the DFS, if it is an edge mark dist[row][col] = 1 and add element to row queue/col queue. Else mark dist[row][col] = -1.
- Then do a BFS. 
  - Nodes are considered during bfs if:
    - nodes are within bounds of the matrix
    - dist[row][col] == 0
  - If matrix[row][col] == 1 we have found the edge of second island and we return distance
  
--------

### Question 216: Linked List Deletion
Declare a head, prev and current. Set current to node and while it is not null do the following - while current.val = target, increment current. If current is not null increment both prev and current. Return head.next.

--------

### Question 49: Longest Increasing Subsequence
DP problem. Let `f(i)` be LIS from `i...n` such that `a[i]` is included.

```
f(i) = 1 // if i = a.length
f(i) = max(i, f(j) ) // for j = i+1 ... n && a[i] < a[j]
```
Return the max f(i).

----------

### Question 52: Autobots, combine!
Convert int array to string array. Then sort the array using custom comparator `Arrays.sort(a, c)`. The custom comparator takes 2 strings `a, b` and compares `a+b` with `b+a`.

We can use the `string1.compareTo(sring2)` to return the answer. If `string1` > `string2`, positive number s returned else negative number is returned.

----------

### Question 117: H-Index
Sort the array. If `a[i] >= a.length - i` it means there are at least `a.length - i` elements with `i` citations. To find the best possible value of i, do a binary search.

---------

### Question 121: Sudoku Validator
Use hashset to check rows, check cols and check grids. In addition to uniqueness we must make sure `a[i][j]` is between `1...9`.

-------
