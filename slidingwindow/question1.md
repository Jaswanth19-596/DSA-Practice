# 594. Longest Harmonious Subsequence

## EASY

We define a harmonious array as an array where the difference between its maximum value and its minimum value is exactly 1.

Given an integer array nums, return the length of its longest harmonious subsequence among all its possible subsequences.

### Examples:

```Example 1:

Input: nums = [1,3,2,2,5,2,3,7]

Output: 5

Explanation:

The longest harmonious subsequence is [3,2,2,2,3].
```

```
Example 2:

Input: nums = [1,2,3,4]

Output: 2

Explanation:

The longest harmonious subsequences are [1,2], [2,3], and [3,4], all of which have a length of 2.
```

```
Example 3:

Input: nums = [1,1,1,1]

Output: 0

Explanation:

No harmonic subsequence exists.
```

```
### Constraints:

1 <= nums.length <= 2 \* 104
-109 <= nums[i] <= 109
```

### Observations

- We cannot have more than 2 different numbers in our subsequence.
- These two numbers should be adjacent numbers (Because the difference should be 1)
- Does the order matter: No, we are just considering length of subseqeunce and not the order.

### Appraoch 1:

- Basically try to think that what this question is trying to do with your mind, its more of a mind game here.
  So basically you just have to find a number and then the successor(number +1 ) of that number in the given array and check their frequencies and that will be our answer.(Why?)

  ````Algorithm findLHS(nums):

  Input: An array nums storing n ≥ 1 integers.
  Output: The length of the longest harmonious subsequence.

  1. freq ← Empty HashMap
  2. for each num in nums do
     if num exists in freq then
     freq[num] ← freq[num] + 1
     else
     freq[num] ← 1
  3. res ← 0
  4. for each key in freq.keys() do
     if freq contains (key + 1) then
     res ← max(res, freq[key] + freq[key + 1])
  5. return res

  Time Complexity: O(n)
  Space Complexity: O(n)```
  ````

### Approach 2:

    def findLHS(self, nums: List[int]) -> int:

        nums.sort()

        l = 0
        r = 1
        result = 0


        while r < len(nums):

            diff = nums[r] - nums[l]

            if diff == 1:
                result = max(result, r - l + 1)
                r += 1
            elif diff > 1:
                l += 1
            else:
                r +=1

        return result


    Time complexity: O(n)
    Space Complexity: O(n)
