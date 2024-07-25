# 3rd
実際の場面だと、lower_bound のようなコードを書ける自信がなくてこのコードを3段階目に書いた  
理解していれば覚えられるはずなので、まだ理解が浅いということなのか
```cpp
class Solution {
private:
    int searchNum(vector<int>& nums, int target, int left, int right) {
        if(left > right) {
            return -1;
        }
        int mid = left + (right - left) / 2;
        if(nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
            return searchNum(nums, target, left, right);
        } else {
            right = mid - 1;
            return searchNum(nums, target, left, right);
        }
    }
    
public:
    int search(vector<int>& nums, int target) {
        return searchNum(nums, target, 0, nums.size() - 1);
    }
};
```
