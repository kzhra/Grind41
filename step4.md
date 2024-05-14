# step4
レビューで指摘された箇所  
* if-else の繰り返しが多いのでまとめる・拡張性の考慮  
* parentheses の typo  
* forやifの後ろは一つスペースを入れる  
* stack の parenthese という変数名を分かりやすいものに変更  

```cpp
class Solution {
public:
    bool isValid(string s) {
       stack<char> open_parentheses;
       unordered_map<char, char> match_parentheses;
       match_parentheses['('] = ')';
       match_parentheses['{'] = '}';
       match_parentheses['['] = ']';

       for(char c: s) {
        if (c == '(' || c == '{' || c == '[') {
            open_parentheses.push(c);
        } else if (!open_parentheses.empty() && match_parentheses[open_parentheses.top()] == c) {
            open_parentheses.pop();
        } else {
            return false;
        }
       }
       return open_parentheses.empty();
    }
};
```
