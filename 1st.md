# 1st
通るまでに結構間違えた  
事前に自分でテストケースを作って確認するのが足りなかった
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {

       map<char, int> count_letter_1; // counting_letter, letters_to_count
       map<char, int> count_letter_2;

       for (char c : s) {
          ++count_letter_1[c];
       }
       for (char c : t) {
          ++count_letter_2[c];
       }

       // アナグラムの判定, s に存在する文字が t に同数含まれているか
       for (auto& i : count_letter_1) {
          char c = i.first;
          int count_1 = i.second;
          if (count_letter_2.find(c) == count_letter_2.end() || 
              count_1 != count_letter_2[c]) {
                  return false;
          }
        }

        // t に存在して、s に存在しない文字があるかチェック、 s = a, t = ab
       for (const auto& i : count_letter_2) {
          char c = i.first;
          if (count_letter_1.find(c) == count_letter_1.end()) {
              return false;
          }
       }
       return true;
    }
};
```
