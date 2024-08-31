# step1
```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> bracketsStack;  

        for(char c: s) {
            // open brackets の場合
            if(c == '(' || c == '{' || c == '[') {
                bracketsStack.push(c);
                continue;
            }
            // close brackets の場合
            if(c == ')') {
                if(!bracketsStack.empty() && bracketsStack.top() == '(') {
                    bracketsStack.pop();
                    continue;
                }
                return false;
            }
            if(c == '}') {
                if(!bracketsStack.empty() && bracketsStack.top() == '{') {
                    bracketsStack.pop();
                    continue;
                }
                return false;
            }
            if(c == ']') {
                if(!bracketsStack.empty() && bracketsStack.top() == '[') {
                    bracketsStack.pop();
                    continue;
                }
                return false;
            }
        }
        // 例えば (){
        if(bracketsStack.size()) {
            return false;
        }
        return true;
    }
};
```

# step2
step1 の条件判定を short-circuit evaluation　でネストを下げた  
参照  
https://github.com/NobukiFukui/Grind75-ProgrammingTraining/pull/4  
https://github.com/Kitaken0107/GrindEasy/pull/5  
https://discord.com/channels/1084280443945353267/1195700948786491403/1198133880834768896  
https://github.com/colorbox/leetcode/pull/4  
https://github.com/hayashi-ay/leetcode/pull/16   
https://github.com/shining-ai/leetcode/pull/6  

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> bracketsStack;  

        for(char c: s) {
            // open brackets の場合
            if(c == '(' || c == '{' || c == '[') {
                bracketsStack.push(c);
                continue;
            }
            // close brackets の場合
            if(c == ')' && !bracketsStack.empty() && bracketsStack.top() == '(') {
                bracketsStack.pop();
                continue;
            }
            if(c == '}' && !bracketsStack.empty() && bracketsStack.top() == '{') {
                bracketsStack.pop();
                continue;
            }
            if(c == ']' && !bracketsStack.empty() && bracketsStack.top() == '[') {
                bracketsStack.pop();
                continue;
            }
        }
        // 例えば s = "(){"
        if(bracketsStack.size()) {
            return false;
        }
        return true;
    }
};
```

# step3
変数名をジェネリックプログラミングの観点から型名を除去    
if continue から if else に変更  
条件判定で最初に empty を判定。理由は覚えていないが多分計算量を少しでも減らすため？代わりに可読性の低下 
```cpp
class Solution {
public:
    bool isValid(string s) {
       stack<char> parenthese;

       for(char c: s) {
        if(c == '(' || c == '{' || c == '[') {
            parenthese.push(c);
        } else if(!parenthese.empty() && c == ')' && parenthese.top() == '(') {
            parenthese.pop();
        } else if(!parenthese.empty() && c == '}' && parenthese.top() == '{') {
            parenthese.pop();
        } else if(!parenthese.empty() && c == ']' && parenthese.top() == '[') {
            parenthese.pop();
        } else {
            return false;
        }
       }
       return parenthese.empty();
    }
};
```
