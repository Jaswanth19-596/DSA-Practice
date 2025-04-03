# 3191. Minimum Operations to Make Binary Array Elements Equal to One I

## MEDIUM

You are given a binary array nums.

You can do the following operation on the array any number of times (possibly zero):

Choose any 3 consecutive elements from the array and flip all of them.
Flipping an element means changing its value from 0 to 1, and from 1 to 0.

Return the minimum number of operations required to make all elements in nums equal to 1. If it is impossible, return -1.

### Examples:

```
Example 1:

Input: nums = [0,1,1,1,0,0]

Output: 3

Explanation:
We can do the following operations:

Choose the elements at indices 0, 1 and 2. The resulting array is nums = [1,0,0,1,0,0].
Choose the elements at indices 1, 2 and 3. The resulting array is nums = [1,1,1,0,0,0].
Choose the elements at indices 3, 4 and 5. The resulting array is nums = [1,1,1,1,1,1].
```

```
Example 2:

Input: nums = [0,1,1,1]

Output: -1

Explanation:
It is impossible to make all elements equal to 1.
```

```
### Constraints:

3 <= nums.length <= 105
0 <= nums[i] <= 1
```

### Observations

- The subarray element should be of length 3.

### Appraoch 1:

    - Just traverse the array.
    - If you encounter a 0, then flip the next consecutive 3 elements.
    - If there is a zero that cannot be flipped, it will move to the last two positions.
    - Check last two positions, and if there is a zero return -1.
    - Else return the count of flips.

    def minOperations(self, nums: List[int]) -> int:
        count = 0
        for i in range(0, len(nums) - 2):

            currElement = nums[i]

            if currElement == 0:
                count += 1
                nums[i] = 1 - nums[i]
                nums[i+1] = 1 - nums[i+1]
                nums[i+2] = 1 - nums[i+2]

        for i in range(len(nums) - 2, len(nums)):
            if nums[i] == 0:
                return -1

        return count




    Time Complexity: O(n)
    Space Complexity: O(1)

```

```
