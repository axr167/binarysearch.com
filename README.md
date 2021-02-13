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

### Question 17: Run-Length Encoding
Itertate through the string keeping track of the count.

--------

### Question 123: A Maniacal Walk
DP problem the recurrence is as follows:

```
f(i, n) = 1 // if i = 0 && n == 0
f(i, n) = 0 // if n = 0
f(i, n) = f(i+1, n-1) + f(i-1, n-1) + f(i, n-1) // if 0 < i < length-1
f(i, n) = f(i+1, n-1) + f(i, n-1) // if i = 0
f(i, n) = f(i-1, n-1) + f(i, n-1) // if i = length-1
```

The trick is to mod it properly by 1000000007 (which I did not do and so I had to look at the editorial). I need to revise modular arithmetic.

---------

### Question 114: Edit Distance
DP problem. Recurrence is below:

```
f(i,j) = 0 // if i=s1.length and j=s2.length
f(i,j) = s2.length - j // if i = s1.length
f(i,j) = s1.length - i // if j = s2.length
f(i,j) = min( f(i,j+1)+1, f(i+1, j)+1, f(i+1, j+1)+1 ) // if s1[i] != s2[j]
f(i,j) = min( f(i,j+1)+1, f(i+1, j)+1, f(i+1, j+1) ) // if s1[i] = s2[j]
```

--------

### Question 115: Merge New Interval

2 intervals a, b intersect if: 1st point of a is between points of b; 2nd point of a is between points of b; 1st point of b is between points of a; 2nd point of b is between points of a.

Maintain a boolean variable `added` which will be set to true if we have added the target interval to the result. Then iterate over the intervals.

- If `!added` and target interval's end point is less than current interval's start point, add both intervals to result and set `added` to true.
- Else if target intersects the current interval, set `target[0] = min(target[0], current[0])` and `target[1] = max(target[1], current[1])`
- Else there is no intersection so add current interval to result.

In the end if `added` is still false, add `target` to result.

-----------

### Question 766: Rolling Median

Maintain a max heap and a min heap. The min heap has the lesser half of all the elements and the max heap has the greater half of all the elements.

When adding:
- If the element is less than `max.peek()` then it belongs to the lesser half. Add to max heap.
- Else if the element is greater than `max.peek()` then it belongs to greater half. Add to min heap.
- Finally rebalance the heaps such that the diff between the sizes is at most 1.

When calling getMedian():
- If a heap has more elements return the `peek()` value from the heap with more elements
- Otherwise get the `peek()` value from both heaps and divide by 2

-----------

### Question 16: Labyrinthian Possibilities

DP problem. Recurrence is below:

```
if(i == m-1 && j == n-1)
    f(i, j) = 1
if(i == m || j == n)
    f(i, j) = 0
if(a[i][j] == 1)
    f(i, j) = 0
else
    f(i, j) = f(i+1, j) + f(i, j+1)
```

Note that we need to mod by 1000000007.

----------

### Question 154: Friend Groups

**NOTE:** This problem is incorrect because there are 2 contradicting test cases: `friends = [[0, 1], [1]], expected = 1` and `friends = [[0], [0, 1]], expected = 2`.
- If the first example is the correct one, we should find number of strongly connected components in a directed graph - Kosaraju can be used for this. 
- If the second example is correct, we should just assume edges are bidirectional and use union find/dfs for this.

To show as completed, I just copy/pasted a random example from solutions.

--------

### Question 1: Sum of Two Numbers

Initialize set and traverse through list. If set contains `k - nums[i]` return true. Otherwise add `nums[i]` in the set. Return false in the end.

---------

### Question 6: Special Product Array

Declare result array, fill it with 1s then get cumulative array from left and cumulative array from right like so:

```
product = nums[0];
for(int i=1; i<nums.length; i++) {
    res[i] = res[i] * product;
    product = product * nums[i];
}
        
product = nums[nums.length-1];
for(int i = nums.length-2; i>=0; i--) {
    res[i] = res[i] * product;
    product = product * nums[i];
}
```

--------

### Question 7: First Missing Positive

Add all items of array to a hashset. Initialize result to 1. While set contains result, increment result. Finally return result.

---------

### Question 11: Longest Substring with K Distinct Characters

Standard 2 pointer problem that uses map for storing additional info. Start p1 and p2 at index 0. While p2 < str.length()-1 do the following:
- increment p2 and add the character/count pair to the hashmap.
- While `map.size() > k` remove the char at `p1` from the map and increment the left pointer
- Keep track of max substring length by doing `max(max, p2-p1+1)`

------------

### Question 12: Collecting Coins

DP problem same as min path sum. Recurrence is below. It can be solved with `n^2` time `n` space.

```
f(i, j) = a[i][j] // if i = a.length-1 and j = a[0].length-1
f(i, j) = a[i][j] + f(i+1, j) // if j = a[0].length-1
f(i, j) = a[i][j] + f(i, j+1) // if i = a.length-1
f(i, j) = a[i][j] + max(f(i+1, j), f(i, j+1)) // otherwise
```

----------

### Question 13: Mad Max

We need to find maximum over a sliding window of k elements. This is a monotonic queue problem where we have a decreasing monotonic queue for k elements and the max element is in the end of the queue (since it is decreasing). 
- First we fill in the queue with first k elements and set `res[0] = deque.peekLast()` - this is us filling the window initially.
- Then we slide the window from `i = k to i = a.length-1`
  - if `deque.peekLast() == a[i-k]` then remove last element by doing `deque.removeLast()`
  - Add `a[i]` to the queue, increment the index and set `res[index] = deque.peekLast()`


------------

### Question 22: Number of Islands

Scan the matrix. Each time a `1` is encountered, increment the count and do a dfs.

------------


### Question 67: Binary Search Tree Validation

define `f(node, min, max)` where node.val has to be between min and max. If node is null return true. If the node val does not lie between min and max return false. Return the AND of node.left and node.right.


-------------

### Question 123: Longest Increasing Path

DP problem. Define `f(i, j)` as the longest increasing path from `a[i][j]` - this is stored in the DP array. Recurrence is:

    f(i, j) = 1 + max( f(i+1, j), f(i-1, j), f(i, j+1), f(i, j-1) )

Notes about the above recurrence:
- If i and j in `f(i, j)` is out of bounds, `f(i, j) = 0`
- We simply do not process the recurrence for values where `f(i+1, j)` etc are less than `f(i, j)` - the recurrence is done only for increasing neighbours.
  - For decreasing neighbours we use 0 instead.
  
-----------

### Question 110: Rocketship Rescue

2 pointer problem. Sort the array and set 2 pointers - one from start (i) the other from the end (j). Then while i <= j  do the following:

- If i == j, put weights[i] on a ship and decrement j
- Else if weights[i] + weights[j] <= limit, put both weights of i and j on a ship. increment i and decrement j
- Else put weights[j] on a ship and decrement j

Problem assumes no single person's weight is more than rocketship limit

--------------

### Question 104: Remove Duplicate Numbers

**Note:** Number of unique numbers != number of elements with no repititions. If we have `[0,0,1,2]`, number of unique numbers is `[0,1,2]` but number of elements with no repititions is `[1,2]`.

The idea is to maintain two hashsets. First hashsets has uniques and the other has duplicates. Then iterate over array and do the following:

- If `a[i]` does not exist in either one of the hashsets, add it to uniques
- If `a[i]` exists in uniques then remove it from uniques and put it in duplicates

Initialize `res` array of length `uniques.size()` and do a second pass through the array adding `a[i]` in res if it is in uniques.

---------------

### Question 216: Edges that Disconnect the Graph

Tarjan's bridge finding algorithm is used here. 
I have made a video covering the intuition [here](https://www.youtube.com/watch?v=ehNrssKX7wA)

----------------

### Question 105: Postfix Notation Evaluation
Use stack. If it is a number push the number into stack. If it is an operator, pop 2 elements from the stack, do the operation and push the result in the stack

**Note:** Use a stack of type Long. I was using stack of type int and I got wrong answer because of under/overflow - this is tricky to debug in java and I had no idea why my solution was incorrect until I unlocked editorials.

-----------------

### Question 8: Decode Message
DP problem. Define `f(i)` as number of ways to decode `string[i...end]`. The recurrence is as follows:

```
f(i) = 1 // if i = s.length()
f(i) = 0 // if s[i] = 0
f(i) = f(i+1) + f(i+2) // if Integer.parseInt( s.substring(i, i+2) ) <=26
f(i) = f(i+1) // otherwise
```

This can be solved in `O(n)` time and `O(1)` space bottom up.

**Note:** Be careful about the edge case in recurrence #3. We also need to add a check making sure that `i+1 < message.length()` to avoid out of bounds exception.

----------------

### Question 215: Linked List Deletion

Create head node and set `head.next = root`. Set `current = head` and while `current.next` is not null do the following:
- If `current.next.val == target` then set `current.next = current.next.next`
- Else set `current = current.next`

-----------------

### Question 266: Number of Hops

Two ways to do this problem. **Solution 1** is an `O(n^2)` time `O(n)` space solution that uses DP. Define f(i) as the number of hops to get to last position from `i`. Recurrence is below.

```
f(i) = 0 // if i = a.length-1
f(i) = max // if a[i] = 0
f(i) = 1 + min(f(i+1)...f(i+a[i])) // otherwise
```
An edge case is that in recurrence 3, the min could be `max` so we need to be careful we dont add 1 to it. This solution **works for leetcode but gives a TLE for binarysearch** hence we need to use solution 2.

**Solution 2** is BFS based and `O(n)` time with constant space. Keep track of: 
- The index we need to make a jump from - this is initially set to 0. This represents all the elements reachable from 1 bfs jump.
- The max possible index we can reach - this is `Math.max(max, i+a[i])`
- The count of jumps so far

Since there is a guarantee that we will always reach the end we can do the following: 
- loop over the list of nums and update the max possible index we can reach - this represents a BFS run.
- If this is greater than `nums.length-1` make a jump from the current index and return number of jumps.
- Otherwise if `i == index_to_jump_from`
 - Make a jump
 - Set `index_to_jump_from = max`
 
---------------

### Question 52: Zipped String
DP problem. Recurrence is below.

```
let k be index for c. we can get k's value by doing i+j
        
f(i, j) = true // if i = a.length && j == b.length
if i == a.length
    f(i, j) = false // if b[j] != c[k]
    f(i, j) = f(i, j+1) // otherwise
if j == b.length
    f(i, j) = false // if a[i] != c[k]
    f(i, j) = f(i+1, j) // otherwise
f(i, j) = false // if a[i] != c[k] && b[j]  != c[k]
f(i, j) = f(i+1, j) || f(i, j+1) // if a[i] = b[j] = c[k]
f(i, j) = f(i+1, j) // if a[i] = c[k]
f(i, j) = f(i, j+1) // if b[j] = c[k]
```

This can be done in `O(n^2)` time and `O(n)` space.

--------------

### Question 101: Longest Consecutive Duplicate String

Use variables max to keep track of max substring seen so far with duplicates and current which keeps track of current duplicate count. Set max = current = 1 then iterate over string from index `1...s.length()`.

- If `s.charAt(i) == s.charAt(i-1)` then set `current += 1` and `max = max(max, current)`
- Else it means we are at new char. Set `current = 1`
- Return max in the end

--------------

### Question 42: Bipartite Graph

Two coloring problem - this is an application of bfs. Iterate over all nodes. If `visited[node] == 0` mark `visited[node] = 1` and start a bfs at node.

In the bfs do the following:

- Add initial node to queue and while queue is not empty pop the queue - let the popped element be `current`
- For each child of current if `visited[child] != 0 && visited[child] != -1 * visited[current]` there is a violation and graph is not bipartite.
- Otherwise if `visited[child] == 0` then set `visited[child] = visited[current] * -1`

---------------

### Question 84: Break String Into Words

DP problem. Here we define `f(i, j)` as a function that returns true if `s[i...s.length-1]` can be split into words. The variable j represents the end of the substring we are currently looking at.

The recurrence is as follows:

```
f(s, i, j) = true // if i = s.length
f(s, i, j) = false // if j = s.length
f(s, i, j) = f(s, j+1, j+1) || f(s, i, j+1) // if set.contains(s[i...j])
f(s, i, j) = f(s, i, j+1) // otherwise
```

Note: Bottom up gives TLE so use topdown

---------------

### Question 159: Merging K Sorted Lists

Can be done in 2 ways. Method 1 is to use a min heap and keep popping stuff. Method 2 is to use divide and conquer which is explained here. Define 2 functions: 
- The first is `f1(int[] a, int[] b)` that creates a new list `int[] res = new int[a.length+b.length]` which contains the sorted elements of a and b.
- The second is `f2(int lo, int hi, int[][] lists)` that takes all the lists from `lists[lo] ... lists[hi]` and stores them in `lists[lo]`
  - if `lo == hi` it is the base case so return `lists[lo]`
  - Else do `mid = (lo+hi)/2` and do the following:
    - lists[lo] = f2(lo, mid, lists) and lists[mid] = f2(lo, mid, lists)
    - lists[lo] = f1(lists[lo], lists[mid]) and return lists[lo].
- In the end return `lists[0]`

---------------

### Question 77: Merging Two Sorted Lists

Function f1 from above

-----------

### Question 27: Longest Common Subsequence

DP problem. We define `f(i, j)` as LCS for substrings from `s1[i...n]` and `s2[j...n]`. Recurrence below:

```
f(i, j) = 0 // if i == s1.length || j == s2.length
f(i, j) = max(1+f(i+1, j+1), f(i+1, j), f(i, j+1))  // if s1[i] == s2[j]
f(i, j) = max(f(i+1, j), f(i, j+1))
```

-------------


### Question 205: Longest Common Substring

DP problem. We define `f(i, j)` as LCS for substrings from `s1[i...n]` and `s2[j...n]` where the substrings start at i and j. This means unlike the previous problem, the LCS needs to start at `s[i]` and `s[j]` for each computation. The recurrence is below:

```
f(i, j) = 0 // if i == s1.length || j == s2.length
f(i, j) = 1 + f(i+1, j+1) // if s1[i] == s2[j]
f(i, j) = 0 // if s1[i] != s2[j]

return max f(i, j)
```

-------------

### Question 95: Detecting an Odd Length Cycle

Do a BFS on each unvisited node keeping track of the index. If a node tries to visit an already visited node, its a cycle. We can check the number of nodes in the cycle by doing `index[node] - index[alreadyVisitedNode]`. If this number is odd, we can return true.

----------

### Question 215: Distributed Systems

Dijkstra's algorithm. The small text here is that nodes are bidirectional so if we have `[0, 1, 2]` in the edge list, we also need to create an entry for `[1, 0, 2]`

----------
