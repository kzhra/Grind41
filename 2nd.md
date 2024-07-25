# 2-1
lower_bound を実装
```cpp
class Solution {
private:
    template<typename Iterator, typename T>
    Iterator myLowerBound(Iterator first, Iterator last, const T& value) {
        Iterator it;
        typename std::iterator_traits<Iterator>::difference_type count, step;
        count = std::distance(first, last);

        while(count > 0) {
            it = first;
            step = count / 2;
            std::advance(it, step);
            if(*it < value) {
                first = ++it;
                count -= step + 1;
            } else {
                count = step;
            }
        }
        return it;
    }


    int findTarget(const vector<int>& data, int target) {
    auto it = myLowerBound(data.begin(), data.end(), target);
    if (it != data.end() && *it == target) {
        return std::distance(data.begin(), it);  // 要素が見つかったインデックスを返す
    }
    return -1;  // 要素が見つからなかった
}
    
public:
    int search(vector<int>& nums, int target) {
        return findTarget(nums, target);
    }
};
```


# 2-2
参考  
https://github.com/rm3as/code_interview/pull/9
```cpp
class Solution {
private:
    int findTarget(const vector<int>& nums, int target) {
        int low = 0;
        int high = nums.size() - 1;
        while(low < high){
            int middle = (low + high) / 2;
            if (target > nums[middle]){
                low = middle + 1;
            } else {
                high = middle;
            }
        }
        return low;
    }
    
public:
    int search(vector<int>& nums, int target) {
        int index = findTarget(nums, target);
        if (index < nums.size() && nums[index] == target) {
            return index; 
        } else {
            return -1; 
        }
    }
};
```
