# 4th
sort

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        // 場合によっては別の変数に移してから sort 
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        return s == t;
    }
};
```
