# 413. Arithmetic Slices

## MEDIUM

An integer array is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, [1,3,5,7,9], [7,7,7,7], and [3,-1,-5,-9] are arithmetic sequences.
Given an integer array nums, return the number of arithmetic subarrays of nums.

A subarray is a contiguous subsequence of the array.

### Examples:

```
Example 1:

Input: nums = [1,2,3,4]
Output: 3
Explanation: We have 3 arithmetic slices in nums: [1, 2, 3], [2, 3, 4] and [1,2,3,4] itself.
```

```
Example 2:

Input: nums = [1]
Output: 0
```

```
### Constraints:

1 <= nums.length <= 5000
-1000 <= nums[i] <= 1000
```

### Observations

- The subarray should contain atleast 3 elements.
- The difference between the elements in the subarray should be equal.

### Appraoch 1:

    - Bruteforce through all the subarrays and count the Arithmetic slices.

    Time Complexity: O(n^2)
    Space Complexity: O(1)

```

### Approach 2:

    Two pointer approach.

    # First I'll be having two pointers
        # start, end
        # I will keep the start at the starting position and end at first element and get their diff in a diff varaible.
        # Now i will move the end pointer till the diff between end and end - 1 ! = diff.
        # if end - (end - 1) != diff:
            # num = end - start
            # count += (num * (num + 1)/2)
            # start = end - 1
            # diff = end - (end - 1)
        # else:
            # end += 1

    class Solution:
    def numberOfArithmeticSlices(self, nums: List[int]) -> int:

        if len(nums) < 3:
            return 0


        start = 0
        end = 1

        diff = nums[end] - nums[start]

        count = 0
        while(end < len(nums)):

            newDiff = nums[end] - nums[end - 1]

            if newDiff != diff:

                numberOfElements = (end - start) - 2
                if numberOfElements >= 0:
                    count += ((numberOfElements * (numberOfElements + 1)) // 2)

                start = end - 1

                diff = newDiff
            else:
                end += 1

        numberOfElements = (end - start) - 2
        if numberOfElements >= 0:
            count += ((numberOfElements * (numberOfElements + 1)) // 2)
        return count

    Time complexity: O(n)

    Space Complexity: O(1)
```

### Approach 3:

    public int numberOfArithmeticSlices(int[] A) {
    int curr = 0, sum = 0;
    for (int i=2; i<A.length; i++)
        if (A[i]-A[i-1] == A[i-1]-A[i-2]) {
            curr += 1;
            sum += curr;
        } else {
            curr = 0;
        }
    return sum;

    }

```

```
