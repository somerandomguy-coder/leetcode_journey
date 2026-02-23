 # 📝 DSA Batch Log: Week 1, theme: leetcode from zero

## Problem 1: Longest Palindromeic Substring, https://leetcode.com/problems/longest-palindromic-substring

Status: Stuck at Level 3 (trying to optimize from O(n^3) to less)

### My Intuition (Level 1 - Visual/Logic): 
* 2 pointers, left and right, check every single substring

### The Idea (Level 2 - Strategy): 
* sometimes when see the current substring is smaller than longest, directly skip it, or if submitted that substring to become the longest, don't need to check the smaller substring of it 

### Complexity: 
* Time: $O(n^3)$Space: $O(1)$

### The Code (C++ / Python):

```
# C++ 
class Solution {
public:
    string longestPalindrome(string s) {
        // Time: O(n^3: n*n*window_size)
        // Space: O(1)

        int right = s.length()-1;
        int left_shadow = 0;
        int right_shadow = right;

        int current_length = 0;
        int longest = 1;
        string result = s.substr(0,1);

        // left pointer move from start
        for (int left=0; left<s.length(); left++) {
            while (right > left) {
                std::cout << "left: "<< left << "," << s[left] << ", right: " << right << "," << s[right] << "\n";
                if (s[left] == s[right]) {
                    std::cout << "left == right" << "\n";
                    left_shadow = left;
                    right_shadow = right;
                    current_length = right_shadow - left_shadow + 1;
                    // if the current_length are not longer than longest, no more reason to check if it's valid
                    if (current_length < longest) {
                        goto end_of_loop;
                    } 
                    // check if the window is valid, if left and right next to each other or point at the same index + have the same value, it's a valid window
                    while (right_shadow != left_shadow && right_shadow != left_shadow + 1) {
                         left_shadow++; 
                         right_shadow--;
                         // invalid window
                        if (s[left_shadow] != s[right_shadow]){
                            std::cout << "invalid substring right here" << "\n";
                            current_length = 0;
                            break;
                        }
                        
                    }
                    // if current_length = 0, means the window is not valid, otherwise keep going to compare
                    // if length is larger than the current longest, get the new longest substring
                    std::cout << current_length << "," << longest << "\n";
                    if (current_length > longest) {
                        longest  = current_length;
                        result = s.substr(left, current_length);

                        // if found good result, move onto next loop, because the substring can't be longer than the substring containing it
                        goto end_of_loop;
                    }
                    
                }
                // move right pointer to the left 
                right--;
            }

            end_of_loop:;
            // at the end of 1 loop, reset right pointer
            right = s.length()-1;
        }
        return result;
    }
};
```

### The "Innovation" Question: 
* What is the best way to check if it's palindrome or not?
