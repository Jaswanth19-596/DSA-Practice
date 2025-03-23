# 1984. Minimum Difference Between Highest and Lowest of K Scores

## EASY

You are given a 0-indexed integer array nums, where nums[i] represents the score of the ith student. You are also given an integer k.

Pick the scores of any k students from the array so that the difference between the highest and the lowest of the k scores is minimized.

Return the minimum possible difference.

### Examples:

```
Example 1:

Input: nums = [90], k = 1
Output: 0
Explanation: There is one way to pick score(s) of one student:
- [90]. The difference between the highest and lowest score is 90 - 90 = 0.
The minimum possible difference is 0.
```

```
Example 2:

Input: nums = [9,4,1,7], k = 2
Output: 2
Explanation: There are six ways to pick score(s) of two students:
- [9,4,1,7]. The difference between the highest and lowest score is 9 - 4 = 5.
- [9,4,1,7]. The difference between the highest and lowest score is 9 - 1 = 8.
- [9,4,1,7]. The difference between the highest and lowest score is 9 - 7 = 2.
- [9,4,1,7]. The difference between the highest and lowest score is 4 - 1 = 3.
- [9,4,1,7]. The difference between the highest and lowest score is 7 - 4 = 3.
- [9,4,1,7]. The difference between the highest and lowest score is 7 - 1 = 6.
The minimum possible difference is 2.
```

```
### Constraints:

1 <= k <= nums.length <= 1000
0 <= nums[i] <= 105
```

### Observations

    - Choose k elements out of the n elements, and find the difference.
    - This difference should be minimum.

    - The elements should be as close as possible for the difference to be minimum.
    - Sorting the array is the best option.

### Appraoch 1:

- 1. Sort the array
  2. Generate all possible substrings of length k.
  3. For every substring => Find differnce between min and max elements.
  4. Keep track of minimum difference.

```
    Time Complexity: O(nlogn) + O(n^2)
    Space Complexity: O(1)
```

### Approach 2:

    - For every substring, we don't really care about inbetween elements.
    - We only care about the highest and smallest element which in this case are the ith and i - k th element after sorting.
    - So, we can just slide the window over and then keep track of the difference.

    def minimumDifference(self, nums: List[int], k: int) -> int:
        # The order of the k students doesn't matter

        if k == 1:
            return 0

        nums.sort()

        i = 0

        for i in range(k-1):
            i += 1

        res = nums[i] - nums[i-k + 1]

        for i in range(k, len(nums)):
            res = min(res, nums[i]- nums[i-k + 1])
            i+=1

        return res


    Time complexity: O(nlogn) + O(n)

    Space Complexity: O(1)
