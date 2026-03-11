 # 📝 DSA Batch Log: Week 4, Theme: leetcode from zero 

## Problem 10: Regular Expression Matching
https://leetcode.com/problems/regular-expression-matching/description/

Status: Stuck at Level 2 

### My Intuition (Level 1 - Visual/Logic): 
* I imagine parsing both side at the same time and if parsing '.' then continue, if see ' * ' check for the next word and check for how many words are there. if there's 5 characters similar to the next character then we do that much amount of case. it will result in O(n!) time

### The Idea (Level 2 - Strategy): 
* I actually stucked

### Complexity: 
* Time: $O(n!)$Space: $O(min(m, n))$

### The Code (C++ / Python):

```
# C++ 
class Solution {
public:
    bool isMatch(string s, string p) {
        // check for quick false lens
        int stars {0};
        for (char charr : p) {
            if (charr == '*') {
                ++stars;
            }
        }
        if (stars == 0) {
            if (s.length != p.length) {
                return false;
            }
        }

        // chop it by index;
        int above = 0;
        int below = 0;
        char next_char {};
        const int LENGTH = p.length()
        int count {};
        while (above < LENGTH) {
            if (p[above] == '.'){
                if (below <= s.length()){ //in case it's at the end 
                    ++above;
                    ++below;
                    continue;
                } else {
                    return false;
                }
            } else if (p[above] == '*'){
                if (above + 1 < p.length()){
                    next_char = p[above+1];
                    count = 0;
                    for (int i=below; i<s.length(); ++i){
                        if (s[i] == next_char) count++;
                    }
                    if (count == 0) return false;
                    for (int i = 0; i < count; ++i){
                        
                    }
                } else {
                    return true; // if * at the end of p, anything in s from that point would pass
                }
            } else if (p[above] == s[below]){
                ++above;
                ++below;
                continue;
            } else {
                return false;
            }
        }
        return true;
    }
};

```

### The "Innovation" Question: 
