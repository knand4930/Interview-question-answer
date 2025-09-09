# Complete DSA Practice Sets - Detailed Problems

## 1. Primitive Data Structures

### Integer Operations

#### Problem 1: Check if Number is Prime
**Problem Statement:** Given an integer n, determine whether it is a prime number or not. A prime number is a natural number greater than 1 that has no positive divisors other than 1 and itself.

**Input Format:** 
- Single integer `n` (1 ≤ n ≤ 10^6)

**Output Format:** 
- Return `True` if n is prime, `False` otherwise

**Examples:**
```
Input: n = 17
Output: True
Explanation: 17 has no divisors except 1 and 17

Input: n = 15
Output: False  
Explanation: 15 = 3 × 5, so it has divisors other than 1 and 15
```

**Algorithm:** Trial Division with Optimization
**Approach:** 
1. Handle edge cases (n ≤ 1, n = 2, even numbers)
2. Check divisibility from 3 to √n with step 2 (only odd numbers)
3. If any divisor found, return False; otherwise True

**Time Complexity:** O(√n)  
**Space Complexity:** O(1)

---

#### Problem 2: Find GCD of Two Numbers (Euclidean Algorithm)
**Problem Statement:** Find the Greatest Common Divisor (GCD) of two positive integers using the Euclidean algorithm.

**Input Format:** 
- Two integers `a` and `b` (1 ≤ a, b ≤ 10^9)

**Output Format:** 
- Return the GCD of a and b

**Examples:**
```
Input: a = 48, b = 18
Output: 6
Explanation: Factors of 48: 1,2,3,4,6,8,12,16,24,48
            Factors of 18: 1,2,3,6,9,18
            Common factors: 1,2,3,6
            Greatest: 6

Input: a = 17, b = 13
Output: 1
Explanation: Both are prime, so GCD is 1
```

**Algorithm:** Euclidean Algorithm
**Approach:** 
1. If b = 0, return a
2. Otherwise, return GCD(b, a % b)
3. Continue until b becomes 0

**Time Complexity:** O(log(min(a,b)))  
**Space Complexity:** O(1) iterative, O(log(min(a,b))) recursive

---

#### Problem 3: Convert Binary to Decimal
**Problem Statement:** Given a binary string, convert it to its decimal equivalent.

**Input Format:** 
- String `binary` containing only '0' and '1' (1 ≤ length ≤ 32)

**Output Format:** 
- Return decimal equivalent as integer

**Examples:**
```
Input: binary = "1010"
Output: 10
Explanation: 1×2³ + 0×2² + 1×2¹ + 0×2⁰ = 8 + 0 + 2 + 0 = 10

Input: binary = "1111"
Output: 15
Explanation: 1×2³ + 1×2² + 1×2¹ + 1×2⁰ = 8 + 4 + 2 + 1 = 15
```

**Algorithm:** Horner's Method / Positional Notation
**Approach:** 
1. Initialize result = 0
2. For each bit from left to right: result = result × 2 + current_bit
3. Return result

**Time Complexity:** O(n) where n is length of binary string  
**Space Complexity:** O(1)

---

### String Operations

#### Problem 4: Check if String is Palindrome
**Problem Statement:** Determine whether a given string is a palindrome. A palindrome reads the same forward and backward.

**Input Format:** 
- String `s` (1 ≤ length ≤ 10^5)

**Output Format:** 
- Return `True` if palindrome, `False` otherwise

**Examples:**
```
Input: s = "racecar"
Output: True
Explanation: "racecar" reads same forwards and backwards

Input: s = "hello"
Output: False
Explanation: "hello" backwards is "olleh"

Input: s = "A man a plan a canal Panama"
Output: True (considering only alphanumeric, case insensitive)
```

**Algorithm:** Two Pointer Technique
**Approach:** 
1. Use two pointers: left at start, right at end
2. Compare characters at both pointers
3. Move pointers toward center
4. If any mismatch found, return False

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

#### Problem 5: Find First Non-Repeating Character
**Problem Statement:** Given a string, find the first non-repeating character and return its index. If it doesn't exist, return -1.

**Input Format:** 
- String `s` (1 ≤ length ≤ 10^5)

**Output Format:** 
- Return index of first non-repeating character, or -1 if none exists

**Examples:**
```
Input: s = "leetcode"
Output: 0
Explanation: 'l' appears only once and is the first such character

Input: s = "loveleetcode"
Output: 2
Explanation: 'v' is the first character that appears only once

Input: s = "aabb"
Output: -1
Explanation: All characters repeat
```

**Algorithm:** Hash Map (Frequency Count)
**Approach:** 
1. First pass: Count frequency of each character
2. Second pass: Find first character with frequency 1
3. Return its index or -1 if not found

**Time Complexity:** O(n)  
**Space Complexity:** O(1) - at most 26 characters for lowercase English

---

## 2A. Linear Data Structures

### Array

#### Problem 6: Find Second Largest Element
**Problem Statement:** Given an array of integers, find the second largest element. If no second largest exists, return -1.

**Input Format:** 
- Array `arr` of integers (1 ≤ length ≤ 10^5)

**Output Format:** 
- Return second largest element or -1

**Examples:**
```
Input: arr = [1, 3, 4, 5, 2]
Output: 4
Explanation: Largest = 5, Second largest = 4

Input: arr = [5, 5, 5]
Output: -1
Explanation: All elements are same

Input: arr = [1, 2]
Output: 1
Explanation: Second largest is 1
```

**Algorithm:** Two-Pass or Single-Pass
**Approach:** 
1. Track first_max and second_max
2. Iterate through array once
3. Update maximums appropriately
4. Handle duplicates correctly

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

#### Problem 7: Rotate Array by K Positions
**Problem Statement:** Rotate an array to the right by k steps, where k is non-negative.

**Input Format:** 
- Array `nums` (1 ≤ length ≤ 10^5)
- Integer `k` (0 ≤ k ≤ 10^5)

**Output Format:** 
- Modify array in-place or return rotated array

**Examples:**
```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation: 
rotate 1 step: [7,1,2,3,4,5,6]
rotate 2 steps: [6,7,1,2,3,4,5]
rotate 3 steps: [5,6,7,1,2,3,4]

Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
```

**Algorithm:** Reverse Algorithm
**Approach:** 
1. Normalize k: k = k % n
2. Reverse entire array
3. Reverse first k elements
4. Reverse remaining n-k elements

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

#### Problem 8: Subarray with Given Sum
**Problem Statement:** Find a continuous subarray whose sum equals the target sum. Return the starting and ending indices.

**Input Format:** 
- Array `arr` of positive integers
- Target sum `target`

**Output Format:** 
- Return [start_index, end_index] or [-1, -1] if not found

**Examples:**
```
Input: arr = [1,4,2,3,5], target = 7
Output: [1, 3]
Explanation: Subarray [4,2,3] has sum 7, starts at index 1, ends at index 3

Input: arr = [1,2,3,4], target = 10
Output: [0, 3]
Explanation: Entire array sums to 10

Input: arr = [1,2,3], target = 7
Output: [-1, -1]
Explanation: No subarray sums to 7
```

**Algorithm:** Sliding Window Technique
**Approach:** 
1. Use two pointers: start and end
2. Expand window by moving end pointer
3. Shrink window by moving start pointer when sum > target
4. Return indices when sum equals target

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

### Stack (LIFO)

#### Problem 9: Valid Parentheses
**Problem Statement:** Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

**Input Format:** 
- String `s` (0 ≤ length ≤ 10^4)

**Output Format:** 
- Return `True` if valid, `False` otherwise

**Examples:**
```
Input: s = "()"
Output: True

Input: s = "()[]{}"
Output: True

Input: s = "(]"
Output: False

Input: s = "([)]"
Output: False
Explanation: Brackets are not properly nested

Input: s = "{[]}"
Output: True
```

**Algorithm:** Stack-based Matching
**Approach:** 
1. Push opening brackets onto stack
2. For closing brackets, check if stack top matches
3. Pop matching opening bracket
4. String is valid if stack is empty at end

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

#### Problem 10: Next Greater Element
**Problem Statement:** For each element in the array, find the next greater element. The next greater element is the first greater element to the right.

**Input Format:** 
- Array `nums` (1 ≤ length ≤ 10^4)

**Output Format:** 
- Return array where each position contains next greater element or -1

**Examples:**
```
Input: nums = [1,3,2,4]
Output: [3,4,4,-1]
Explanation: 
- Next greater of 1 is 3
- Next greater of 3 is 4  
- Next greater of 2 is 4
- Next greater of 4 doesn't exist (-1)

Input: nums = [6,8,0,1,3]
Output: [8,-1,1,3,-1]
```

**Algorithm:** Monotonic Stack
**Approach:** 
1. Use stack to store indices of elements
2. For each element, pop smaller elements from stack
3. Current element is next greater for popped elements
4. Push current index to stack

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### Queue (FIFO)

#### Problem 11: Generate Binary Numbers 1 to N
**Problem Statement:** Generate binary representations of numbers from 1 to n using a queue.

**Input Format:** 
- Integer `n` (1 ≤ n ≤ 10^5)

**Output Format:** 
- Return array of binary strings

**Examples:**
```
Input: n = 5
Output: ["1", "10", "11", "100", "101"]
Explanation: 
1 = "1", 2 = "10", 3 = "11", 4 = "100", 5 = "101"

Input: n = 3
Output: ["1", "10", "11"]
```

**Algorithm:** Queue-based Generation
**Approach:** 
1. Start with "1" in queue
2. For each string in queue, generate two new strings by appending "0" and "1"
3. Continue until n numbers are generated
4. Each dequeue operation gives next binary number

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

#### Problem 12: Sliding Window Maximum
**Problem Statement:** Given an array and a sliding window of size k, find the maximum element in each window as it slides from left to right.

**Input Format:** 
- Array `nums` (1 ≤ length ≤ 10^5)
- Window size `k` (1 ≤ k ≤ length)

**Output Format:** 
- Return array of maximum elements in each window

**Examples:**
```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window [1,3,-1] → max = 3
Window [3,-1,-3] → max = 3  
Window [-1,-3,5] → max = 5
Window [-3,5,3] → max = 5
Window [5,3,6] → max = 6
Window [3,6,7] → max = 7

Input: nums = [1], k = 1
Output: [1]
```

**Algorithm:** Deque (Double-ended Queue)
**Approach:** 
1. Use deque to store indices of array elements
2. Maintain deque in decreasing order of values
3. Remove indices outside current window
4. Front of deque always contains index of maximum element

**Time Complexity:** O(n)  
**Space Complexity:** O(k)

---

## 2B. Non-Linear Data Structures

### Binary Tree

#### Problem 13: Binary Tree Maximum Depth
**Problem Statement:** Find the maximum depth of a binary tree. The maximum depth is the number of nodes along the longest path from root to leaf.

**Input Format:** 
- Root of binary tree

**Output Format:** 
- Return maximum depth as integer

**Examples:**
```
Input: [3,9,20,null,null,15,7]
     3
   /   \
  9     20
       /  \
      15   7
Output: 3

Input: [1,null,2]
  1
   \
    2
Output: 2

Input: []
Output: 0
```

**Algorithm:** Recursive DFS or BFS
**Approach (DFS):** 
1. If node is null, return 0
2. Recursively find depth of left and right subtrees
3. Return 1 + max(left_depth, right_depth)

**Time Complexity:** O(n)  
**Space Complexity:** O(h) where h is height

---

#### Problem 14: Binary Tree Level Order Traversal
**Problem Statement:** Given a binary tree, return the level order traversal of its nodes' values (i.e., from left to right, level by level).

**Input Format:** 
- Root of binary tree

**Output Format:** 
- Return 2D array where each sub-array contains nodes of one level

**Examples:**
```
Input: [3,9,20,null,null,15,7]
     3
   /   \
  9     20
       /  \
      15   7
Output: [[3],[9,20],[15,7]]

Input: [1]
Output: [[1]]

Input: []
Output: []
```

**Algorithm:** BFS using Queue
**Approach:** 
1. Use queue to store nodes level by level
2. Process all nodes of current level before moving to next
3. Track level size to separate levels
4. Add node values to result for each level

**Time Complexity:** O(n)  
**Space Complexity:** O(w) where w is maximum width

---

### Binary Search Tree

#### Problem 15: Validate Binary Search Tree
**Problem Statement:** Determine if a binary tree is a valid binary search tree (BST).

**Input Format:** 
- Root of binary tree

**Output Format:** 
- Return `True` if valid BST, `False` otherwise

**Examples:**
```
Input: [2,1,3]
    2
   / \
  1   3
Output: True

Input: [5,1,4,null,null,3,6]
    5
   / \
  1   4
     / \
    3   6
Output: False
Explanation: Node 4 is in left subtree of 5 but 4 > 1 (left child of 5)
```

**Algorithm:** In-order Traversal or Recursive Bounds
**Approach (Bounds):** 
1. For each node, maintain valid range (min, max)
2. Root can be any value: range (-∞, +∞)
3. Left child: range (min, node.val)
4. Right child: range (node.val, max)
5. Check if node value is within valid range

**Time Complexity:** O(n)  
**Space Complexity:** O(h)

---

### Heap

#### Problem 16: Kth Largest Element in Array
**Problem Statement:** Find the kth largest element in an unsorted array. Note that it is the kth largest element in sorted order, not the kth distinct element.

**Input Format:** 
- Array `nums` (1 ≤ length ≤ 10^4)
- Integer `k` (1 ≤ k ≤ length)

**Output Format:** 
- Return kth largest element

**Examples:**
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
Explanation: Sorted array is [1,2,3,4,5,6], 2nd largest is 5

Input: nums = [3,2,3,1,2,4,5,5,6], k = 4  
Output: 4
Explanation: Sorted array is [1,2,2,3,3,4,5,5,6], 4th largest is 4
```

**Algorithm:** Min Heap of size K
**Approach:** 
1. Build min heap of first k elements
2. For remaining elements, if element > heap top:
   - Remove heap top
   - Add current element
3. Heap top is kth largest element

**Time Complexity:** O(n log k)  
**Space Complexity:** O(k)

---

### Graph

#### Problem 17: Course Schedule (Topological Sort)
**Problem Statement:** There are `numCourses` courses labeled 0 to numCourses-1. Given prerequisites array where prerequisites[i] = [ai, bi] indicates you must take course bi first to take course ai. Determine if you can finish all courses.

**Input Format:** 
- Integer `numCourses`
- 2D array `prerequisites`

**Output Format:** 
- Return `True` if possible to finish all courses, `False` otherwise

**Examples:**
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: True
Explanation: Take course 0 first, then course 1

Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: False  
Explanation: Circular dependency - impossible to complete

Input: numCourses = 3, prerequisites = [[1,0],[2,0],[2,1]]
Output: True
Explanation: Take 0, then 1, then 2
```

**Algorithm:** Topological Sort using DFS (Cycle Detection)
**Approach:** 
1. Build adjacency list from prerequisites
2. Use DFS with three states: unvisited, visiting, visited
3. If we encounter a "visiting" node during DFS, cycle exists
4. If no cycle found, all courses can be completed

**Time Complexity:** O(V + E)  
**Space Complexity:** O(V + E)

---

#### Problem 18: Number of Islands
**Problem Statement:** Given a 2D grid of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and formed by connecting adjacent lands horizontally or vertically.

**Input Format:** 
- 2D grid of characters ('0' or '1')

**Output Format:** 
- Return number of islands

**Examples:**
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1

Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

**Algorithm:** DFS or BFS
**Approach (DFS):** 
1. Iterate through each cell in grid
2. When '1' is found, increment island count
3. Use DFS to mark all connected '1's as visited ('0')
4. Continue until entire grid is processed

**Time Complexity:** O(M × N)  
**Space Complexity:** O(M × N) in worst case

---

## 3. Hash-Based Data Structures

#### Problem 19: Two Sum
**Problem Statement:** Given an array of integers and a target sum, return indices of two numbers that add up to target.

**Input Format:** 
- Array `nums` (2 ≤ length ≤ 10^4)
- Target integer `target`

**Output Format:** 
- Return array of two indices

**Examples:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9

Input: nums = [3,2,4], target = 6
Output: [1,2]

Input: nums = [3,3], target = 6
Output: [0,1]
```

**Algorithm:** Hash Map (One Pass)
**Approach:** 
1. Create hash map to store (value → index)
2. For each element, calculate complement = target - current
3. If complement exists in map, return [map[complement], current_index]
4. Otherwise, add current element to map

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

#### Problem 20: Group Anagrams
**Problem Statement:** Given an array of strings, group anagrams together. Anagrams are words formed by rearranging letters of another word.

**Input Format:** 
- Array of strings `strs`

**Output Format:** 
- Return list of groups, where each group contains anagrams

**Examples:**
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Input: strs = [""]
Output: [[""]]

Input: strs = ["a"]
Output: [["a"]]
```

**Algorithm:** Hash Map with Sorted String as Key
**Approach:** 
1. For each string, sort its characters to get signature
2. Use signature as key in hash map
3. Group strings with same signature
4. Return all groups

**Time Complexity:** O(N × K log K) where N = number of strings, K = max string length  
**Space Complexity:** O(N × K)

---

## Algorithm Categories

### Dynamic Programming

#### Problem 21: Longest Increasing Subsequence
**Problem Statement:** Given an integer array, return the length of the longest strictly increasing subsequence.

**Input Format:** 
- Array `nums` (1 ≤ length ≤ 2500)

**Output Format:** 
- Return length of LIS

**Examples:**
```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: LIS is [2,3,7,18] or [2,3,7,101]

Input: nums = [0,1,0,3,2,3]
Output: 4
Explanation: LIS is [0,1,2,3]

Input: nums = [7,7,7,7,7,7,7]
Output: 1
```

**Algorithm:** Dynamic Programming
**Approach:** 
1. dp[i] = length of LIS ending at index i
2. For each i, check all previous elements j where nums[j] < nums[i]
3. dp[i] = max(dp[i], dp[j] + 1)
4. Return max(dp)

**Time Complexity:** O(n²)  
**Space Complexity:** O(n)

---

#### Problem 22: Coin Change
**Problem Statement:** Given coins of different denominations and a total amount, find the minimum number of coins needed to make up that amount. If impossible, return -1.

**Input Format:** 
- Array `coins` of coin denominations
- Target amount `amount`

**Output Format:** 
- Return minimum coins needed or -1

**Examples:**
```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

Input: coins = [2], amount = 3
Output: -1

Input: coins = [1], amount = 0
Output: 0
```

**Algorithm:** Dynamic Programming (Bottom-up)
**Approach:** 
1. dp[i] = minimum coins needed for amount i
2. dp[0] = 0, dp[i] = infinity for i > 0
3. For each amount from 1 to target:
   - Try each coin denomination
   - dp[amount] = min(dp[amount], dp[amount-coin] + 1)
4. Return dp[amount]

**Time Complexity:** O(amount × coins)  
**Space Complexity:** O(amount)

---

### Backtracking

#### Problem 23: N-Queens Problem
**Problem Statement:** Place n queens on an n×n chessboard such that no two queens attack each other. Return all distinct solutions.

**Input Format:** 
- Integer `n` (1 ≤ n ≤ 9)

**Output Format:** 
- Return list of all valid board configurations

**Examples:**
```
Input: n = 4
Output: [
 [".Q..",
  "...Q", 
  "Q...",
  "..Q."],
 ["..Q.",
  "Q...",
  "...Q",
  ".Q.."]
]

Input: n = 1
Output: [["Q"]]
```

**Algorithm:** Backtracking with Constraint Checking
**Approach:** 
1. Place queens row by row
2. For each row, try placing queen in each column
3. Check if placement is safe (no conflicts with previous queens)
4. If safe, recursively solve for next row
5. If solution found, add to result; otherwise backtrack

**Time Complexity:** O(N!)  
**Space Complexity:** O(N²)

---

### Greedy Algorithms

#### Problem 24: Activity Selection Problem
**Problem Statement:** Given start and end times of activities, select maximum number of activities that can be performed by a single person, assuming a person can only work on a single activity at a time.

**Input Format:** 
- Array `start[]` of start times
- Array `end[]` of end times

**Output Format:** 
- Return maximum number of activities

**Examples:**
```
Input: start = [1,3,0,5,8,5], end = [2,4,6,7,9,9]
Output: 4
Explanation: Select activities (1,2), (3,4), (5,7), (8,9)

Input: start = [10,12,20], end = [20,25,30] 
Output: 2
Explanation: Select activities (10,20), (20,30)
```

**Algorithm:** Greedy - Sort by End Time
**Approach:** 
1. Sort activities by their end times
2. Select first activity
3. For remaining activities, select if start time ≥ end time of last selected
4. Count total selected activities

**Time Complexity:** O(n log n)  
**Space Complexity:** O(1)

---

### Divide and Conquer

#### Problem 25: Maximum Subarray (Kadane's Algorithm vs Divide & Conquer)
**Problem Statement:** Find the contiguous subarray with the largest sum and return its sum.

**Input Format:** 
- Array `nums` of integers (-10^4 ≤ nums[i] ≤ 10^4)

**Output Format:** 
- Return maximum subarray sum

**Examples:**
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: Subarray [4,-1,2,1] has sum = 6

Input: nums = [1]
Output: 1

Input: nums = [5,4,-1,7,8]
Output: 23
```

**Algorithm:** Divide and Conquer
**Approach:** 
1. Divide array into two halves
2. Maximum subarray is either:
   - Entirely in left half
   - Entirely in right half  
   - Crosses the middle point
3. Recursively find max in left and right halves
4. Find max crossing sum by extending from middle
5. Return maximum of three values

**Time Complexity:** O(n log n)  
**Space Complexity:** O(log n)

---

## Practice Guidelines & Tips

### Problem-Solving Framework:
1. **Understand**: Read problem carefully, identify constraints
2. **Examples**: Work through examples manually  
3. **Approach**: Start with brute force, then optimize
4. **Edge Cases**: Consider empty inputs, single elements, duplicates
5. **Implement**: Write clean, readable code
6. **Test**: Verify with examples and edge cases
7. **Optimize**: Analyze time/space complexity

### Common Patterns:
- **Two Pointers**: Sorted arrays, palindromes
- **Sliding Window**: Subarray problems with conditions
- **Hash Maps**: O(1) lookups, frequency counting
- **Stack**: Parentheses, next greater/smaller
- **Queue/BFS**: Level-order, shortest path
- **DFS**: Tree traversal, connected components
- **DP**: Optimal substructure, overlapping subproblems
- **Binary Search**: Sorted data, search space

### Complexity Analysis:
- Always analyze both time and space complexity
- Consider best, average, and worst cases
- Understand trade-offs between time and space
- Know when to use iterative vs recursive solutions
