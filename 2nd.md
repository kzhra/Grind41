# 2nd
# 2-1
map を1つの使用に減らした  
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
       // s = "a", t = "ab" の場合どうすればいいか、一致すれば --map[]として最後にmap[] ==  0 かチェック

       map<char, int> count_char_s;  
       for (const auto& c : s) {
            ++count_char_s[c];
       } 

       for (const auto& c : t) {
            // 追記、contains の方がよかった
            if (count_char_s.find(c) != count_char_s.end()) {
                --count_char_s[c];
            } else {
                return false;
            }
       }

       // s = "ab", t = "a" のような場合の検証
       for (const auto& item : count_char_s) {
            int count = item.second;
            if (count != 0) {
                return false;
            }
       }
       return true;
    }
};
```

# 2-2
初期化と比較の for 文を1つにまとめた
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) {
            return false;
        }

        map<char, int> count;  
        for (int i = 0; i < s.length(); ++i) {
            ++count[s[i]];
            --count[t[i]];
        }

        for (auto& pair : count) {
            if (pair.second != 0) {
                return false;
            }
        }
        return true;
    }
};

```
