 # 📝 DSA Batch Log: Week 4, theme: leetcode from zero 
 
## Problem 8: String to Integer (atoi)
https://leetcode.com/problems/string-to-integer-atoi/description/

Status: Solved 

### My Intuition (Level 1 - Visual/Logic): 
* Streaming the number

### The Idea (Level 2 - Strategy): 
* Have multiple flag to flag out if sign have taken if white space have taken if sign is negative,...

### Complexity: 
* Time: $O(n)$Space: $O(1))$

### The Code (C++ / Python):

```
# C++ 
class Solution {
public:
    int myAtoi(string s) {
        int sign {1};
        bool sign_exist {false};
        bool num {false};
        int result {0};
        int digit;
        for (char charr : s) {
            if (charr == ' ' && sign_exist == false && num==false) {
                continue;
            } else if (charr == ' ' && (sign_exist == true || num == true)){
                break;
            } else if ((charr == '-' || charr == '+') && sign_exist == true) {
                break;
            } else if (charr == '+' && num == false){
                sign_exist = true;
            } else if (charr == '-' && num == false){
                sign = -1;
                sign_exist = true;
            } else if (std::isdigit(charr)) {
                num = true;
                digit = charr - '0';
                if (sign == 1 && (result > INT_MAX/10 || ((result == INT_MAX/10) && digit > 7))){
                    return INT_MAX;
                } else if (result < INT_MIN/10 || ((result == INT_MIN/10) && sign*digit < -8)){
                    return INT_MIN;
                } else {
                    result = result*10 + sign*digit;
                }
            } else {
                break;
            }
        }
    return result;
    }
};
```

### The "Innovation" Question: 
Should I organize it better? like if see white space then do the checking nested inside it, so I won't have 2 duplicate check for white space and some flag? 
Is there better option than streaming?

Answer: Yes, you can do it like phase check, phase 1 check for whitespace, phase 2 check for sign, phase 3 check for number, that way we don't need to look back to phase 1 if already passed
