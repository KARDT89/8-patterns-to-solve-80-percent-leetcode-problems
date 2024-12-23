# LeetCode Patterns

This repository covers 8 essential patterns that can help solve 80% of LeetCode problems. Each pattern includes a brief explanation, example problems, and code snippets.

## 1. Sliding Window

### Description
The sliding window pattern is used to perform a required operation on a contiguous subset of elements in an array or string.

### Example Problems
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

### Code Snippet
```python
def lengthOfLongestSubstring(s: str) -> int:
    n = len(s)
    char_set = set()
    left = 0
    max_length = 0

    for right in range(n):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)

    return max_length
```

## 2. Two Pointers

### Description
Two pointers technique involves using two indices to traverse the array, which can help solve problems involving pairs or subsets in linear time.

### Example Problems
- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- [3Sum](https://leetcode.com/problems/3sum/)
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

### Code Snippet
```python
def twoSum(numbers: List[int], target: int) -> List[int]:
    left, right = 0, len(numbers) - 1

    while left < right:
        current_sum = numbers[left] + numbers[right]
        if current_sum == target:
            return [left + 1, right + 1]
        elif current_sum < target:
            left += 1
        else:
            right += 1

    return []
```

## 3. Fast and Slow Pointers

### Description
This pattern uses two pointers moving at different speeds to detect cycles in linked lists or to find the middle element.

### Example Problems
- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
- [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

### Code Snippet
```python
def hasCycle(head: ListNode) -> bool:
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True

    return False
```

## 4. Binary Search

### Description
Binary search is a divide-and-conquer algorithm that finds the position of a target value within a sorted array.

### Example Problems
- [Binary Search](https://leetcode.com/problems/binary-search/)
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

### Code Snippet
```python
def binarySearch(nums: List[int], target: int) -> int:
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

## 5. Backtracking

### Description
Backtracking is an algorithmic technique for solving problems recursively by trying to build a solution incrementally.

### Example Problems
- [Permutations](https://leetcode.com/problems/permutations/)
- [Combination Sum](https://leetcode.com/problems/combination-sum/)
- [Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)

### Code Snippet
```python
def permute(nums: List[int]) -> List[List[int]]:
    result = []

    def backtrack(start=0):
        if start == len(nums):
            result.append(nums[:])
            return

        for i in range(start, len(nums)):
            nums[start], nums[i] = nums[i], nums[start]
            backtrack(start + 1)
            nums[start], nums[i] = nums[i], nums[start]

    backtrack()
    return result
```

## 6. Dynamic Programming

### Description
Dynamic programming (DP) is a method for solving complex problems by breaking them down into simpler subproblems and storing the results.

### Example Problems
- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- [Coin Change](https://leetcode.com/problems/coin-change/)

### Code Snippet
```python
def climbStairs(n: int) -> int:
    if n <= 2:
        return n

    dp = [0] * (n + 1)
    dp[1], dp[2] = 1, 2

    for i in range(3, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]

    return dp[n]
```

## 7. Greedy Algorithms

### Description
Greedy algorithms make the locally optimal choice at each stage with the hope of finding the global optimum.

### Example Problems
- [Jump Game](https://leetcode.com/problems/jump-game/)
- [Partition Labels](https://leetcode.com/problems/partition-labels/)
- [Gas Station](https://leetcode.com/problems/gas-station/)

### Code Snippet
```python
def canJump(nums: List[int]) -> bool:
    max_reach = 0

    for i, num in enumerate(nums):
        if i > max_reach:
            return False
        max_reach = max(max_reach, i + num)

    return True
```

## 8. Graph Traversal

### Description
Graph traversal algorithms are used to visit all the nodes in a graph. The two most common techniques are Breadth-First Search (BFS) and Depth-First Search (DFS).

### Example Problems
- [Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [Clone Graph](https://leetcode.com/problems/clone-graph/)
- [Course Schedule](https://leetcode.com/problems/course-schedule/)

### Code Snippet (BFS)
```python
def numIslands(grid: List[List[str]]) -> int:
    if not grid:
        return 0

    rows, cols = len(grid), len(grid[0])
    visited = set()
    islands = 0

    def bfs(r, c):
        queue = collections.deque()
        visited.add((r, c))
        queue.append((r, c))

        while queue:
            row, col = queue.popleft()
            directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

            for dr, dc in directions:
                r, c = row + dr, col + dc
                if (r in range(rows) and
                    c in range(cols) and
                    grid[r][c] == '1' and
                    (r, c) not in visited):
                    visited.add((r, c))
                    queue.append((r, c))

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1' and (r, c) not in visited:
                bfs(r, c)
                islands += 1

    return islands
```

### Code Snippet (DFS)
```python
def cloneGraph(node: 'Node') -> 'Node':
    if not node:
        return node

    old_to_new = {}

    def dfs(node):
        if node in old_to_new:
            return old_to_new[node]

        copy = Node(node.val)
        old_to_new[node] = copy

        for neighbor in node.neighbors:
            copy.neighbors.append(dfs(neighbor))

        return copy

    return dfs(node)
```

---

