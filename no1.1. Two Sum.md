# Step1
2重ループで足していくやり方  
時間計算量 O(n^2)  
空間計算量 O(1)  
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for(int i = 0; i < nums.size() - 1; i++) {
            for(int j = i + 1; j < nums.size(); j++) {
                if(target == nums[i] + nums[j]) {
                    return {i, j};
                }
            }
        }
        return {};
    }
};

```

# Step2
unordered_map を使用するものに変更  
count が contains でよかったと後から思う  
時間計算量 O(n)  
空間計算量 O(n)  
参照  
https://github.com/colorbox/leetcode/pull/3  
https://github.com/cheeseNA/leetcode/pull/1  
https://github.com/Kitaken0107/GrindEasy/pull/4  
https://github.com/tshimosake/arai60/blob/master/hash/two_sum.py  
https://github.com/usatie/leetcode/tree/main/Arai60/01.%20Two%20Sum  
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> u_map;
        
        for(int i = 0; i < nums.size(); ++i) {
            u_map[nums[i]] = i;
        }

        for(int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            if(u_map.count(complement) && i != u_map[complement]) {
                return {i, u_map[complement]};
            }
        }

        // target が見つからなかった場合
        return {};
    }
};
```


# Step3
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> nums_to_index_map;
        for(int i = 0; i < nums.size(); ++i) {
            nums_to_index_map[nums[i]] = i;
        }
        for(int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            if(nums_to_index_map.count(complement) && i != nums_to_index_map[complement]) {
                return { i, nums_to_index_map[complement]};
            }
        }
        return {};
    }
};
```
