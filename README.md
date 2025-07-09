#Leetcode Array Solution in Python
## Max Consecutive Ones - Leetcode 485

## Problem Summary
Given a binary array `nums` (only containing 0s and 1s), return the maximum number of consecutive 1s in the array.

## Key Knowledge Points
### 1. Array Traversal Techniques
- **`for num in nums:`**  
  Simple iteration over elements; most readable when only values are needed.  
  Example:
  ```python
  for num in [1, 0, 1]:
      print(num)
  ```

- **`for index, element in enumerate(nums):`**  
  Access both index and value simultaneously; useful when the position matters.  
  Example:
  ```python
  for i, val in enumerate([1, 0, 1]):
      print(f"Index: {i}, Value: {val}")
  ```

- **`for i in range(len(nums)):`**  
  Traditional loop using indices; helpful if you need to compare with neighbors.  
  Example:
  ```python
  nums = [1, 0, 1]
  for i in range(len(nums)):
      if i > 0 and nums[i] == nums[i-1]:
          print(f"nums[{i}] and nums[{i-1}] are the same")
  ```

### 2. Variable Initialization
- `count = 0`: Tracks current streak of 1s.
- `max_count = 0`: Tracks the longest streak found.

### 3. Dynamic Update
- Use `max_count = max(max_count, count)` to continually update the result during traversal.

## Approach
Traverse the array once. For each 1 encountered, increase the count of current consecutive 1s. 
If a 0 is found, reset the count to 0. At each step, compare and update the maximum streak using `max()`.

---

## Python Code
```python
class Solution(object):
    def findMaxConsecutiveOnes(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # Initialize counters
        count = 0
        max_count = 0

        # Traverse the array using: for num in nums
        for num in nums:
            if num == 1:
                # Increase current streak count
                count += 1
            else:
                # Reset current streak count
                count = 0

            # Update max streak if current is higher
            max_count = max(max_count, count)

        return max_count
```

---

## Tags
`Array` `Traversal` `Greedy` `Beginner` `Python` `Leetcode`

---

Feel free to ⭐ this repo if you found it helpful!
