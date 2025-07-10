# Leetcode Array Solution in Python
## ✅ Leetcode 485 — Max Consecutive Ones

---

### 🧩 Problem Summary
Given a binary array `nums` (only containing 0s and 1s), return the maximum number of consecutive 1s in the array.

```python
Input: nums = [1,1,0,1,1,1]
Output: 3  # Because the maximum number of consecutive 1s is three
```

---

### 📚 Key Knowledge Points

#### 1. Array Traversal Techniques
- **`for num in nums:`**  
  Simple iteration over elements.  
  Example:
  ```python
  for num in [1, 0, 1]:
      print(num)
  ```

- **`for index, element in enumerate(nums):`**  
  Access both index and value simultaneously.  
  Example:
  ```python
  for i, val in enumerate([1, 0, 1]):
      print(f"Index: {i}, Value: {val}")
  ```

- **`for i in range(len(nums)):`**  
  Traditional index-based loop.  
  Example:
  ```python
  nums = [1, 0, 1]
  for i in range(len(nums)):
      if i > 0 and nums[i] == nums[i-1]:
          print(f"nums[{i}] and nums[{i-1}] are the same")
  ```

#### 2. Variable Initialization
- `count = 0`: Tracks the current streak of 1s.
- `max_count = 0`: Tracks the longest streak found so far.

#### 3. Dynamic Update
- Use `max_count = max(max_count, count)` to update the result at each step.

---

### 🧠 Approach
#### One-Pass Counter Update

**Core Idea:**
- Traverse the list once.
- If current number is 1, increment `count`.
- If current number is 0, reset `count = 0`.
- After each update, compare with `max_count` and update if needed.

This ensures:
- O(n) time complexity (single traversal)
- O(1) space complexity (only two counters used)

---

### 📝 Step-by-Step Example
```python
nums = [1, 1, 0, 1, 1, 1]

# Initial: count = 0, max_count = 0

# num = 1 → count = 1 → max_count = 1
# num = 1 → count = 2 → max_count = 2
# num = 0 → count = 0 → max_count = 2
# num = 1 → count = 1 → max_count = 2
# num = 1 → count = 2 → max_count = 2
# num = 1 → count = 3 → max_count = 3

# Final result: 3
```

---

### ✅ Python Code with Comments
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

        # Traverse the array
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

### ✅ Summary
- Use a simple pass through the array.
- Count consecutive 1s and track the maximum.
- No extra space required — only counters.
- Great problem to master **array traversal + conditional counting**.

## ✅ Leetcode 1 — Two Sum

---

### 🧩 Problem Summary
Given an integer array `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

You **must** return exactly one solution, and **you may not use the same element twice**.

```python
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]  # Because nums[0] + nums[1] == 9
```

---

### 📚 Key Knowledge Points

#### 1. Hash Map (Dictionary) for Constant-Time Lookup
- Dictionaries in Python offer **O(1)** average time complexity for insert and lookup.
- We use a dict to **store previously seen numbers** and their indices.

```python
seen = {}
seen[2] = 0  # number 2 seen at index 0
```

#### 2. Complement Logic
If `num + complement = target`, then `complement = target - num`.

At each step, we check:
> 🔍 "Have I seen `target - num` before?"
>
> If yes → That’s the pair!

#### 3. Order of Operations Matters
You must check the `complement` **before** storing `num` into the hashmap.
Otherwise, you might return the same index twice.

#### 4. Enumeration
To access both value and index, use `enumerate()`:
```python
for i, num in enumerate(nums):
    ...
```

#### 5. Edge Cases
- Only one solution is guaranteed — no need to handle multiple answers.
- Cannot use the same index twice: `[i, j]` with `i ≠ j`.

---

### 🧠 Approach
#### One-Pass Hash Map

**Core Idea:**
- Traverse the list once, for each `num`, calculate its `complement = target - num`.
- Check if complement is in `seen`. If so, return `[seen[complement], i]`.
- Otherwise, store `num` with its index in `seen`.

This ensures:
- No nested loop (so it's O(n))
- Space is O(n) for the dictionary

---

### 📝 Step-by-Step Example
```python
nums = [3, 2, 4], target = 6

# i = 0, num = 3, complement = 3
→ not in seen → store: {3: 0}

# i = 1, num = 2, complement = 4
→ not in seen → store: {3: 0, 2: 1}

# i = 2, num = 4, complement = 2
→ 2 in seen at index 1 → return [1, 2]
```

---

### ✅ Python Code with Comments
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        # Dictionary to store seen numbers and their indices
        seen = {}

        # Traverse the array
        for i, num in enumerate(nums):
            # Calculate the needed complement
            complement = target - num

            # If complement is already seen, return the pair
            if complement in seen:
                return [seen[complement], i]

            # Otherwise, store current number and index
            seen[num] = i
```

---

### ✅ Summary
- Use a hash map to **reduce time from O(n²) → O(n)**.
- Carefully handle the **order of storing vs. checking**.
- Great first problem to master **hash maps + complement logic**.

## 🚀 Leetcode 283 - Move Zeroes

---

### 📌 Problem Summary
Given an integer array `nums`, move all `0`'s to the end of it while maintaining the **relative order** of the non-zero elements.

You must perform the operation **in-place** with the **least possible operations**.

```python
Input:  nums = [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]
```

---

### 📚 Key Knowledge Points

#### 1. In-Place Modification
You must not allocate another array. All changes must be done within the original list.

#### 2. Maintain Relative Order
The relative order of the non-zero elements must remain the same.

#### 3. Two-Pointer Pattern
- Pointer `i`: current element in iteration  
- Pointer `last_nonzero_index`: the next position where a non-zero element should be placed

---

### 🧠 Optimal Approach

#### ✅ Algorithm
1. Initialize `last_nonzero_index = 0`
2. Traverse the list from left to right
3. If `nums[i] != 0`:
   - Copy it to `nums[last_nonzero_index]`
   - If `i ≠ last_nonzero_index`, clear `nums[i] = 0`
   - Advance `last_nonzero_index`

#### 🔍 Insight
You're gradually building the "non-zero segment" at the beginning of the list, and pushing zeros to the end as a result.

---

### ✅ Python Code (with comments)
```python
class Solution:
    def moveZeroes(self, nums):
        last_nonzero_index = 0

        for i in range(len(nums)):
            if nums[i] != 0:
                nums[last_nonzero_index] = nums[i]
                if i != last_nonzero_index:
                    nums[i] = 0
                last_nonzero_index += 1
```

---

### ⏱️ Complexity
| Metric            | Value |
|-------------------|--------|
| Time Complexity   | O(n)  |
| Space Complexity  | O(1)  |

---

### 🧪 Example Walkthrough
```python
Input: [0, 1, 0, 3, 12]

Steps:
- i=1: move 1 to index 0, clear index 1 → [1, 0, 0, 3, 12]
- i=3: move 3 to index 1, clear index 3 → [1, 3, 0, 0, 12]
- i=4: move 12 to index 2, clear index 4 → [1, 3, 12, 0, 0]
```

---

### ⚠️ Mistake Log: What I Tried and Why It Failed

#### ❌ Mistake 1: Only increment pointer when moving elements
```python
if nums[i] != 0:
    nums[last_nonzero_index] = nums[i]
    if i != last_nonzero_index:
        nums[i] = 0
        last_nonzero_index += 1
```
**Bug:**
If `i == last_nonzero_index`, the pointer won’t move forward. This causes repeated writes and breaks loop termination.

---

#### ❌ Mistake 2: Prematurely incrementing pointer before conditional check
```python
if nums[i] != 0:
    nums[last_nonzero_index] = nums[i]
    last_nonzero_index += 1

    if i != last_nonzero_index:
        nums[i] = 0
```
**Bug:**
You incremented `last_nonzero_index` too early. `i != last_nonzero_index` is now comparing against the next position, not the current one. This causes some zeros not to be written when they should be.

---

#### ❌ Mistake 3: Combining logic into a single condition
```python
if nums[i] != 0 and i != last_nonzero_index:
    nums[last_nonzero_index] = nums[i]
    nums[i] = 0
    last_nonzero_index += 1
```
**Bug:**
When `i == last_nonzero_index`, this block is skipped entirely, so the pointer doesn’t move forward and the algorithm freezes.

---

### 🧠 Final Takeaways
- Avoid writing `last_nonzero_index += 1` too early or too late — **timing matters!**
- Think carefully about when two pointers are equal vs. unequal
- Try to separate "data movement" from "state update" in your logic
- Debug by tracing small inputs like `[0, 1]`, `[2, 1]`, `[0,0,1]` step by step


---

## Tags
`Array` `Traversal` `Greedy` `Beginner` `Python` `Leetcode`

---

Feel free to ⭐ this repo if you found it helpful!
