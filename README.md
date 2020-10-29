# Problems

### Question 340: Run length Decoding

Characters can be double digit; Remember to use functions like `Character.isDigit` and `Character.getNumericValue` to append to stringbuilder

### Question 267: Number of Hops
Dp problem. Set min to max int, careful about overflow when a[i] = 0.
```
dp[i] = 0 // if i = a.length
dp[i] = 1 + min(dp[i+1] ... dp[i+a[i]]) // otherwise
```

### Question 40: Reverse a Linked List
To do it in O(1) space allocate a new head node at start of the list and make `head.next = node`. While `node.next != null`, make `node.next` the next of head. Return `head.next`

### Question 4: Hoppable
Greedy problem. Loop through all elements of list and maintain max hop length `max`. Update max as `max = max(max, i+nums[i])`. If `max >= len` return true. If `max = i` return false.

### Question 118: Space Battle
Monotonic Queue. Iterate over all elements. Have a boolean variable `canAdd` set to true. While queue is not empty && first element is positive && a[i] is negative, begin loop of destruction. In loop of destruction: 
    
- if abs of a[i] is more than first element, remove element. 
- Otherwise if they are equal, remove first element, make `canAdd = false` and break. 
- Otherwise if abs of a[i] smaller than first element, break
 
If we can still add, add a[i] to front of queue. When we have finished iteration, empty queue into result array.

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
