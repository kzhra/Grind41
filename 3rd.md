# 3rd

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        // 英数字以外を取り除く前処理
        string normalized_string;
        for(const char& c: s) {
            if(isAlNum(c)) {
                normalized_string.push_back(std::tolower(c));    
            } 
        }

        int n = normalized_string.length(); 
        for(int i = 0; i < n / 2; ++i) {
            if(normalized_string[i] != normalized_string[n - 1 - i]) {
                return false;
            }
        }
        return true;
    }

    bool isAlNum(char c) {
        if('a' <= c && c <= 'z') {
            return true;
        } else if ('A' <= c && c <= 'Z') {
            return true;
        } else if ('0' <= c && c <= '9') {
            return true;
        }
        return false;
    }
};

```
