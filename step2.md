# step2-1
最大部分配列和を求める問題に置き換えた  

参照
* https://www.geeksforgeeks.org/stock-buy-sell/?ref=ml_lbp
* https://www.geeksforgeeks.org/maximum-difference-between-two-elements/
* https://github.com/NobukiFukui/Grind75-ProgrammingTraining/pull/8
* https://github.com/colorbox/leetcode/pull/6
* https://github.com/Kitaken0107/GrindEasy/pull/7

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        // Input: prices = [7,1,5,3,6,4]
        // Output: 5 で確認
        if (prices.size() < 2) return 0;

        // 1日ごとの価格の変動を入れる配列
        vector<int> daily_price_change{0};  // [0, -6, 4, -2, 3, -2]
        for(int i = 1; i < prices.size(); ++i) {
            daily_price_change.push_back(prices[i] - prices[i-1]);
        }

        // kadane
        // 変動価格の累積和を作る
        vector<int> cums_of_daily{daily_price_change[0]};   // [0, -6, -2, -4, 1, -1], cumulative sum
        for(int i = 1; i < daily_price_change.size(); ++i) {
            int current_cums = cums_of_daily[i-1] + daily_price_change[i];
            cums_of_daily.push_back(current_cums);
        }

        // 累積和を使って最大値(最大部分配列和)を求める calcurate maximum to use coms
        int max_subarray{cums_of_daily[1] - cums_of_daily[0]};
        int min_cums = cums_of_daily[0];
        for(int i = 0; i < cums_of_daily.size(); ++i) {
            max_subarray = std::max(max_subarray, cums_of_daily[i] - min_cums);
            min_cums = std::min(min_cums, cums_of_daily[i]);
        }

        // データが降順に並んでいた場合の処理
        return max_subarray < 0 ? 0 : max_subarray;

     }
};

```

# step2-2
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int buying_price = prices[0];
        int profit = 0;

        for(const auto& price: prices) {
            if(buying_price > price) {
                // price - buying_price > 0 のとき
                buying_price = price;
            } else {
                // price - buying_price <= 0 のとき
                profit = std::max(profit, price - buying_price);
            }
        }
        return profit;
     }
};
```

# step2-3
step2-2 から if を使わなくしただけ
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
       int buying_price = prices[0];
       int profit = 0;  

       for(const auto& price: prices) {
            profit = std::max(profit, price - buying_price);
            buying_price = std::min(buying_price, price);
       } 
       return profit;
     }
};
```
