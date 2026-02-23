 # 📝 DSA Batch Log: Week 1, theme: leetcode from zero

## Problem 1: Longest Palindromeic Substring (second visit)

Status: Solved 

### My Intuition (Level 1 - Visual/Logic): 
* Check every center when expand outward.

### The Idea (Level 2 - Strategy): 
* Instead of picking center from the start to end, pick it from the middle and try move it to left and right
* Sometimes you start from the middle and it's already the best case, just kinda return the result.

### Complexity: 
* Time: $O(n^2)$Space: $O(1)$

### The Code (C++ / Python):

```
# C++ 
class Solution {
public:
    string longestPalindrome(string s) {
        int center_shadow, left, right, longest_possible;
        int center = s.length()/2;
        int start = 0;
        int end = 0;
        int length = 1;
        int longest = 1;
        string result;
        const int LAST_INDEX = s.length()-1;
        
        // move the center from the center to the right
        while (center <= LAST_INDEX){
            std::cout << "start: " << left << ", " << right << "\n";
            left = center - 1;
            right = center + 1;
            center_shadow = center;
            longest_possible = min(((LAST_INDEX-center)*2)+1, (center*1)+2);
            std::cout << longest_possible << "," << longest << "\n";
            // if already find best case, it's done for the day
            if (longest_possible < longest) {
                break;
            }
            // odd palindrome case
            if (left >=0 && right <= LAST_INDEX && center_shadow >= 0 && center_shadow <= LAST_INDEX){

                while (s[left] == s[right] && left >= 0 && right <= LAST_INDEX) {
                    if (right - left + 1 > longest) {
                        start = left;
                        end = right;
                        longest = end - start + 1;
                    }
                    std::cout << "odd: " << left << ", " << right << "\n";
                    left--;
                    right++;
                    if (left < 0 || right > LAST_INDEX){
                        break;
                    }
                }
            }
            left = center - 1;
            right = center + 1;
            center_shadow = center;
            //even case
            if (left >=0 && center_shadow >= 0 && center_shadow <= LAST_INDEX) {

                while (s[left] == s[center_shadow] && left >= 0 && center_shadow <= LAST_INDEX) {
                    if (center_shadow - left + 1 > longest) {
                        start = left;
                        end = center_shadow;
                        longest = end - start + 1;
                    }
                    std::cout << "even left: " << left << ", " << center_shadow << "\n";   
                    left--;
                    center_shadow++;
                    if (left < 0 || center_shadow > LAST_INDEX){
                        break;
                    }
                }
            }
            left = center - 1;
            right = center + 1;
            center_shadow = center;
            if (right <= LAST_INDEX && center_shadow >= 0 && center_shadow <= LAST_INDEX){

                while (s[center_shadow] == s[right] && center_shadow >= 0 && right <= LAST_INDEX) {
                    if (right - center_shadow + 1 > longest) {
                        start = center_shadow;
                        end = right;
                        longest = end - start + 1;
                    }
                    std::cout << "even right: " << center_shadow << ", " << right << "\n";   
                    center_shadow--;
                    right++;
                    if (center_shadow < 0 || right > LAST_INDEX){
                        break;
                    }
                }
            }
            center++;
        }
        // reset center and move the center from the center to the left
        center = s.length()/2;
        while (center >= 0){
            std::cout << "start: " << left << ", " << right << "\n";
            left = center - 1;
            right = center + 1;
            center_shadow = center;
            std::cout << longest_possible << "," << longest << "\n";
            longest_possible = min(((LAST_INDEX-center)*2)+1, (center*2)+1);
            if (longest_possible < longest) {
                break;
            }
            // odd palindrome case
            if (left >=0 && right <= LAST_INDEX && center_shadow >= 0 && center_shadow <= LAST_INDEX){

                while (s[left] == s[right] && left >= 0 && right <= LAST_INDEX) {
                    if (right - left + 1 > longest) {
                        start = left;
                        end = right;
                        longest = end - start + 1;
                    }
                    std::cout << "odd: " << left << ", " << right << "\n";
                    left--;
                    right++;
                    if (left < 0 || right > LAST_INDEX){
                        break;
                    }
                }
            }
            left = center - 1;
            right = center + 1;
            center_shadow = center;
            //even case
            if (left >=0 && center_shadow >= 0 && center_shadow <= LAST_INDEX) {

                while (s[left] == s[center_shadow] && left >= 0 && center_shadow <= LAST_INDEX) {
                    if (center_shadow - left + 1 > longest) {
                        start = left;
                        end = center_shadow;
                        longest = end - start + 1;
                    }
                    std::cout << "even left: " << left << ", " << center_shadow << "\n";   
                    left--;
                    center_shadow++;
                    if (left < 0 || center_shadow > LAST_INDEX){
                        break;
                    }
                }
            }
            left = center - 1;
            right = center + 1;
            center_shadow = center;
            if (right <= LAST_INDEX && center_shadow >= 0 && center_shadow <= LAST_INDEX){

                while (s[center_shadow] == s[right] && center_shadow >= 0 && right <= LAST_INDEX) {
                    if (right - center_shadow + 1 > longest) {
                        start = center_shadow;
                        end = right;
                        longest = end - start + 1;
                    }
                    std::cout << "even right: " << center_shadow << ", " << right << "\n";   
                    center_shadow--;
                    right++;
                    if (center_shadow < 0 || right > LAST_INDEX){
                        break;
                    }
                }
            }
            center--;
        }
        result = s.substr(start, longest);
        return result;
    }
};
```

### The "Innovation" Question: 
* Cleaner way to handle invalid index instead of just keep on checking and checking.
