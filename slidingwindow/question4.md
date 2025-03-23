# 1763. Longest Nice Substring

## EASY

A string s is nice if, for every letter of the alphabet that s contains, it appears both in uppercase and lowercase. For example, "abABB" is nice because 'A' and 'a' appear, and 'B' and 'b' appear. However, "abA" is not because 'b' appears, but 'B' does not.

Given a string s, return the longest substring of s that is nice. If there are multiple, return the substring of the earliest occurrence. If there are none, return an empty string.

### Examples:

```
Example 1:

Input: s = "YazaAay"
Output: "aAa"
Explanation: "aAa" is a nice string because 'A/a' is the only letter of the alphabet in s, and both 'A' and 'a' appear.
"aAa" is the longest nice substring.
```

```
Example 2:

Input: s = "Bb"
Output: "Bb"
Explanation: "Bb" is a nice string because both 'B' and 'b' appear. The whole string is a substring.
```

```

Example 3:

Input: s = "c"
Output: ""
Explanation: There are no nice substrings.
```

```
### Constraints:

1 <= s.length <= 100
s consists of uppercase and lowercase English letters.
```

### Observations

### Appraoch 1:

- 1. Generate all possible substrings

     - 2. For every substring:
       - 3. Create a dictionary that has all the alphabets.
       - 4. Traverse the substring and then populate the dictionary.
       - 5. And then again traverse the substring and for every character, check for both small and capital versions.
       - 6. If charater is small : check for character and character - 32
       - 7. If character is capital : check for character and character + 32

```
class Solution:


    def isNiceSubstring(self, string):

        dict1 = {}

        for i in range(26):
            capital = chr(65 + i)
            small = chr(97 + i)

            dict1[capital] = 0
            dict1[small] = 0

        for ch in string:

            dict1[ch] = 1

        for ch in string:

            if ch.islower() and dict1[chr(ord(ch) - 32)] == 0:
                return False

            if ch.isupper() and dict1[chr(ord(ch) + 32)] == 0:
                return False

        return True





    def longestNiceSubstring(self, s: str) -> str:

        longestSubstring = ""
        for i in range(len(s)):
            substr = ""
            for j in range(i, len(s)):
                substr += s[j]

                res = self.isNiceSubstring(substr)

                if res == True and len(substr) > len(longestSubstring):
                    longestSubstring = substr

        return longestSubstring

    Time Complexity: O(n^3)
    Space Complexity: O(52)
```

### Approach 2:

    - Using Divide and Conquer approach

    Idea:

        - The main idea is that, if there is a character which doesn't have it's counter part, then it cannot be included in the substring.
        - So, the Nice substring can either be on the left of the character or on the right of the character.
        - So, call the recursive calls of the left and right side of the character.





    class Solution:


    def func(self, string, start, end):

        if start > end:
            return ""

        if start == end:
            return ""

        freq = {}

        # O(1)
        for i in range(0, 26):

            freq[chr(97 + i)] = 0
            freq[chr(65 + i)] = 0


        # O(n)
        for i in range(start, end + 1):

            freq[string[i]] = 1

        # O(n)
        for i in range(start, end + 1):
            ch = string[i]

            if (ch.islower() and freq[chr(ord(ch) - 32)] == 0) or (ch.isupper() and freq[chr(ord(ch) + 32)] == 0):
                str1 = self.func(string, start, i - 1)
                str2 = self.func(string, i + 1, end)

                if len(str1) >= len(str2):
                    return str1
                else:
                    return str2

        return string[start : end + 1]

    def longestNiceSubstring(self, s: str) -> str:
        res = self.func(s, 0, len(s) - 1)

        return res





    Time complexity: O(n^2)

        In the worst case, each character doesn't have it's counter part causing a split.
        Recurrence Relation : T(n) = T(0) + T(n - 1) + O(n)

        This makes the tree grow for a height of n and at every level we are doing a work of O(n)


    Space Complexity: O(n)

        - Recursive call stack : O(n)
        - Dictionary : O(1)
