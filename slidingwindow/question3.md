# 1652. Defuse the Bomb

## EASY

You have a bomb to defuse, and your time is running out! Your informer will provide you with a circular array code of length of n and a key k.

To decrypt the code, you must replace every number. All the numbers are replaced simultaneously.

If k > 0, replace the ith number with the sum of the next k numbers.
If k < 0, replace the ith number with the sum of the previous k numbers.
If k == 0, replace the ith number with 0.
As code is circular, the next element of code[n-1] is code[0], and the previous element of code[0] is code[n-1].

Given the circular array code and an integer key k, return the decrypted code to defuse the bomb!

### Examples:

```
Example 1:

Input: code = [5,7,1,4], k = 3
Output: [12,10,16,13]
Explanation: Each number is replaced by the sum of the next 3 numbers. The decrypted code is [7+1+4, 1+4+5, 4+5+7, 5+7+1]. Notice that the numbers wrap around.
```

```
Example 2:

Input: code = [1,2,3,4], k = 0
Output: [0,0,0,0]
Explanation: When k is zero, the numbers are replaced by 0.
```

```

Example 3:

Input: code = [2,4,9,3], k = -2
Output: [12,5,6,13]
Explanation: The decrypted code is [3+9, 2+3, 4+2, 9+4]. Notice that the numbers wrap around again. If k is negative, the sum is of the previous numbers.
```

```
### Constraints:

n == code.length
1 <= n <= 100
1 <= code[i] <= 100
-(n - 1) <= k <= n - 1
```

### Observations

- When k is 0, just return all the elements with 0.
- When k is negative, Return k elements sum from the back.
- when k is positive, return the sum of upcoming k elements.

- When k is positive, just reverse the array and follow the same principles of negative k and at the end reverse the array.

- Solving for negative case:
  - Append the same array at the beginning.
  - Move back k places and find the sum of k elements.
  - Add this sum as first element of the result.
  - Use sliding window to find sum of remaining elements.

### Appraoch 1:

- Append the same array at the beginning.
- Move back k places and find the sum of k elements.
- Add this sum as first element of the result.
- Use sliding window to find sum of remaining elements

```
def func(self, arr, k):

        appended_arr = arr + arr
        n = len(arr)

        i = n - k

        currentSum = 0
        res = []
        for itr in range(i, i + abs(k)):

            currentSum += appended_arr[itr]

        # res.append(currentSum)

        for itr in range(i + abs(k), len(appended_arr)):
            res.append(currentSum)
            currentSum += appended_arr[itr]
            currentSum -= appended_arr[itr-abs(k)]

        return res


    def reverse_array(self, arr):

        i , j = 0, len(arr) - 1

        while( i < j):
            arr[i], arr[j] = arr[j], arr[i]
            i += 1
            j -= 1

        return arr


    def decrypt(self, code: List[int], k: int) -> List[int]:

        if k == 0:
            res = []
            for i in range(len(code)):
                res.append(0)
            return res

        if k > 0:
            arr = self.reverse_array(code)
            res = self.func(arr, k)
            res = self.reverse_array(res)
            return res
        if k < 0:
            res = self.func(code, abs(k))
            return res

    Time Complexity: O(5n)
    Space Complexity: O(n)
```

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
