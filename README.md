# Leetcode_Study_Array
485: Maximum Conseutive Ones
class Solution(object):
    def findMaxConsecutiveOnes(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # Initialize counters:
        # 'count' stores the current streak of consecutive 1s
        # 'max_count' stores the maximum streak found so far
        count = 0
        max_count = 0

        # Traverse the array using the form: for element in list
        for num in nums:
            if num == 1:
                # If the element is 1, increase current streak count
                count += 1
            else:
                # If the element is 0, reset current streak count
                count = 0

            # Update the maximum streak if current streak is longer
            max_count = max(max_count, count)

        return max_count
