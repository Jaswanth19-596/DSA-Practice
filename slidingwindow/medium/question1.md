# 2134. Minimum Swaps to Group All 1's Together II

## MEDIUM

A swap is defined as taking two distinct positions in an array and swapping the values in them.

A circular array is defined as an array where we consider the first element and the last element to be adjacent.

Given a binary circular array nums, return the minimum number of swaps required to group all 1's present in the array together at any location.

### Examples:

```
Example 1:

Input: nums = [0,1,0,1,1,0,0]
Output: 1
Explanation: Here are a few of the ways to group all the 1's together:
[0,0,1,1,1,0,0] using 1 swap.
[0,1,1,1,0,0,0] using 1 swap.
[1,1,0,0,0,0,1] using 2 swaps (using the circular property of the array).
There is no way to group all 1's together with 0 swaps.
Thus, the minimum number of swaps required is 1.

```

```
Example 2:

Input: nums = [0,1,1,1,0,0,1,1,0]
Output: 2
Explanation: Here are a few of the ways to group all the 1's together:
[1,1,1,0,0,0,0,1,1] using 2 swaps (using the circular property of the array).
[1,1,1,1,1,0,0,0,0] using 2 swaps.
There is no way to group all 1's together with 0 or 1 swaps.
Thus, the minimum number of swaps required is 2.
```

```
### Constraints:

1 <= nums.length <= 105
nums[i] is either 0 or 1.
```

### Observations

- The subarray element should be of length 3.

### Appraoch 1:

    This problem of finding the minimum number of swaps to group all 1's in a circular binary array presents a unique challenge due to its circular nature. The key insight is to recognize that we're essentially looking for a contiguous subarray of a specific length (equal to the total number of 1's) that contains the maximum number of 1's.

Given the circular nature of the array, we can visualize it as a ring. The optimal solution will be a segment of this ring that contains the most 1's. The number of swaps needed will be the difference between the total number of 1's and the number of 1's already in this optimal segment.

This problem can be efficiently solved using a sliding window technique, adapted for a circular array. The circular property allows us to consider all possible contiguous segments without explicitly handling different starting positions.

Approach
The solution employs a two-pointer technique combined with a sliding window, adapted for a circular array.

Count Total Ones:

We start by iterating through the array to count the total number of 1's.
This count serves two purposes:
a) It helps us handle edge cases efficiently.
b) It determines the size of our sliding window.
The count is crucial because it represents the size of the group we're trying to form.
Handle Edge Cases:

If there are no 1's in the array, or if all elements are 1's, no swaps are needed.
We can immediately return 0 in these cases, saving unnecessary computations.
Initialize Window:

We create an initial window of size totalOnes.
We count the number of 1's in this initial window.
This window represents our first potential segment where all 1's could be grouped.
Slide the Window:

We use two pointers to slide the window around the circular array.
The sliding process involves:
a) Removing the element at the start of the window.
b) Adding the next element at the end of the window.
We use the modulo operator to wrap around the array, simulating its circular nature.
This clever use of the modulo operator allows us to handle the circular property without creating a duplicate array or using extra space.
Track Maximum:

As we slide the window, we keep track of the maximum number of 1's seen in any window configuration.
This maximum represents the largest group of 1's that already exist contiguously in the array.
Updating this maximum is done in constant time at each step.
Calculate Minimum Swaps:

After sliding the window through all positions, we know the maximum number of 1's that exist contiguously in the array.
The minimum number of swaps is the difference between the total number of 1's and this maximum.
This difference represents the number of 1's that need to be moved to create a contiguous group of all 1's.

```
class Solution {
    public int minSwaps(int[] nums) {
        int n = nums.length;
        int totalOnes = 0;

        // Count total number of 1's
        for (int num : nums) {
            totalOnes += num;
        }

        // Edge cases
        if (totalOnes == 0 || totalOnes == n) return 0;

        int currentOnes = 0;

        // Count 1's in the first window of size totalOnes
        for (int i = 0; i < totalOnes; i++) {
            currentOnes += nums[i];
        }

        int maxOnes = currentOnes;

        // Use two pointers to slide the window
        for (int i = 0; i < n; i++) {
            currentOnes -= nums[i];
            currentOnes += nums[(i + totalOnes) % n];
            maxOnes = Math.max(maxOnes, currentOnes);
        }

        return totalOnes - maxOnes;
    }
}
Time complexity: O(n)
Space complexity: O(1)

```

### Appraoch 2:

    The circular nature of the array suggests that we need to consider all possible contiguous subarrays, including those that wrap around the end of the array.

Approach
Handling Circularity: To address the circular nature of the array, we create a doubled array by concatenating the original array with itself. This allows us to consider all possible contiguous subarrays, including those that wrap around the end of the original array.

Cumulative Sum Array: We construct a cumulative sum array, where each element represents the sum of all elements up to that point in the doubled array. This allows us to calculate the sum of any subarray in constant time.

Window Size: The optimal grouping of 1's will have a size equal to the total number of 1's in the array. We calculate this total as our window size.

Checking All Windows: We iterate through all possible windows of the calculated size, using the cumulative sum array to efficiently determine the number of 1's in each window.

Calculating Swaps: The number of swaps needed for each window is the difference between the total number of 1's and the number of 1's already in the window. The minimum of these differences across all windows is our answer.

Step-by-step breakdown of the algorithm:

Count the total number of 1's in the input array.
Create a doubled array by concatenating the input array with itself.
Construct a cumulative sum array from the doubled array.
Iterate through all possible windows of size equal to the total number of 1's.
For each window, calculate the number of 1's it contains using the cumulative sum array.
Keep track of the maximum number of 1's found in any window.
Return the difference between the total number of 1's and the maximum found in any window.

```
class Solution {
    public int minSwaps(int[] nums) {
        int n = nums.length;
        int totalOnes = 0;

        // Count total number of 1's and create a doubled array
        int[] doubledNums = new int[2 * n];
        for (int i = 0; i < n; i++) {
            totalOnes += nums[i];
            doubledNums[i] = doubledNums[i + n] = nums[i];
        }

        // Edge cases
        if (totalOnes == 0 || totalOnes == n) return 0;

        // Create cumulative sum array
        int[] cumulativeSum = new int[2 * n + 1];
        for (int i = 0; i < 2 * n; i++) {
            cumulativeSum[i + 1] = cumulativeSum[i] + doubledNums[i];
        }

        int maxOnesInWindow = 0;

        // Check all possible windows of size totalOnes
        for (int i = 0; i <= n; i++) {
            int onesInWindow = cumulativeSum[i + totalOnes] - cumulativeSum[i];
            maxOnesInWindow = Math.max(maxOnesInWindow, onesInWindow);
        }

        return totalOnes - maxOnesInWindow;
    }
}

Time complexity: O(n)
Space complexity: O(n)
```
