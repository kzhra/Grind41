単純な2重for文、TLE
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_substract = 0;

        for(int i = 0; i < prices.size() - 1; ++i) {
            int current_max = 0;    
            for(int j = i + 1; j < prices.size(); ++j) {
                current_max = max(current_max, prices[j] - prices[i]); 
            }
            max_substract = max(max_substract, current_max);
        }
        return max_substract;
    }
};
```

答えを見て実装した
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {

        int buying_price = prices[0];
        int selling_price = 0;
        for(int i = 1; i < prices.size(); ++i) {
            if(prices[i] < buying_price) {
                // prices[i] - buying_price < 0 のとき
                buying_price = prices[i];
            } else if(selling_price < prices[i] - buying_price) {
                // prices[i] - buying_price > 0 のとき
                selling_price = max(selling_price, prices[i] - buying_price);
            }
        }
        return selling_price;
    }
};
```
