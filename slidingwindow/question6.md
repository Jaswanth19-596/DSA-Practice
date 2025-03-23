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

- class Solution:
  def divisorSubstrings(self, num: int, k: int) -> int:

        # Create a new variable as a string version of num
        # create n substrings of length k and then convert them to integer and check if it is a divisor.
        # increment the count

        # O(n)
        string = str(num)

        count = 0

        # O(n)
        for i in range(len(string) - k + 1):

            currNum = ""
            # O(k)
            for j in range(i, i + k):

                # O(k)
                currNum += string[j]

                # O(k)
                if int(currNum) == 0:
                    continue

                # O(k)
                if len(currNum) == k and num % int(currNum) == 0:
                    count += 1

        return count

```
    Time Complexity: O(n * k ^2)
    Space Complexity: O(1)
```

### Approach 2:

    def divisorSubstrings(self, num: int, k: int) -> int:

        # create a string variable out of num
        # Keep two pointers i and j  which represent the start and end of window
        # slice from string and then convert to integer and check if it's a divisor

        # O(n)
        string = str(num)

        start = 0
        end = 0

        for i in range(k - 1):
            end += 1


        count = 0

        for i in range(k-1 , len(string)):

            substr = string[start: end + 1]

            if int(substr) != 0 and num % int(substr) == 0:
                count += 1

            start += 1
            end += 1

        return count


    Time complexity: O(n)

    Space Complexity: O(n)
