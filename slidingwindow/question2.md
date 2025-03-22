# 594. Longest Harmonious Subsequence

## EASY

You are given an integer array nums consisting of n elements, and an integer k.

Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10-5 will be accepted.

### Examples:

```
Example 1:

Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75

```

```
Example 2:

Input: nums = [5], k = 1
Output: 5.00000

```

### Constraints:

```
n == nums.length
1 <= k <= n <= 105
-104 <= nums[i] <= 104
```

### Observations

- Values can be both positive and negative.
- All we gotta do is, just add k elements and find the average. And keep track of highest average.

### Corner Cases

- What if k = 1, and n = 1

### Appraoch 1:

```
- Explore each subarray and find the average and keep track of highest average.

 Time Complexity: O(n \* k)
 Space Complexity: O(1)
```

### Approach 2:

    - Use Sliding Window
    - Find the average of first k elements and then keep on sliding the window over the remaining array elements

    class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:

        highestAvg = -100000

        currentSum = 0

        for i in range(k):
            currentSum += nums[i]

        highestAvg = currentSum / k

        for i in range(k, len(nums)):

            currentSum += nums[i]
            currentSum -= nums[i-k]

            highestAvg = max(highestAvg, currentSum / k)

        return highestAvg



    Time complexity: O(n)
    Space Complexity: O(1)
