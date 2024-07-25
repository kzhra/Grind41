# 1st
メソッド名がよくなかった、searchNum とかが適当
```cpp
class Solution {
private:
    int binarySearch(const vector<int>& nums, int target, int left, int right) { 
            if (left > right) {
                return -1; // 探索範囲が無効な場合
            } 

            int index = left + (right - left) / 2;
            if(target == nums[index]) {
                return index;
            } else if (target < nums[index]) {
                return binarySearch(nums, target, left, index - 1);
            } else {
                return binarySearch(nums, target, index + 1, right);
            }
        }
public:
    int search(vector<int>& nums, int target) {
        int last_index = nums.size() - 1;
        return binarySearch(nums, target, 0, last_index);
    }
};
```
