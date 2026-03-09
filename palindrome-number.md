 # 📝 DSA Batch Log: Week 2 theme: leetcode from zero

## Problem 9: Palindrome Number

Status: Solved 

### My Intuition (Level 1 - Visual/Logic): 
* Using the streaming technique from previous to get the exactly inverted number then compare with the original number

### The Idea (Level 2 - Strategy): 
* get the digit by % 10 then divide the original number. the new number will be result * 10 + digit. always check for overflow because int can only be (-2^31, 2^31-1) so always check

### Complexity: 
* Time: $O(n)$Space: $O(1)$

### The Code (C++ / Python):

```
# C++ 
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) return false;
        int invert = 0;
        int y = x;
        int digit;
        int result = 0;
        while (y != 0) {
            digit = y%10;
            y/=10;
            
            // check if its overflow
            if (result > INT_MAX/10 || (result == INT_MAX/10) && digit < 7) return false;
            if (result < INT_MIN/10 || (result == INT_MIN/10) && digit > 8) return false;
            result = result * 10 + digit;
        }
        if (result == x) {
            return true;
        } else {
            return false;
        }
    }
};
```

### The "Innovation" Question: 
is there a better way? without turn it into string ofc

Answer: Yes, if we only stream it halfway (deduce x and until x < palindrome), this way we don't have to check overflow and only go halfway thru
