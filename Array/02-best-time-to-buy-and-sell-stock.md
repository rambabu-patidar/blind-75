# [Best Time To Buy And Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

`Easy` `Array` `Dynamic Programming`

## Key Points

- we can't buy a stock at the last day that will lead to loss
- we can't sell stock on first day because we need to buy on some day and sell it in some future day.

## Approaches

### 1. Keep Track of Maximum price from last and Max Profit Acheived

    Time Complexity: O(N)
    Space Complexity: O(1)

```c++
  class Solution {
  public:
      int maxProfit(vector<int>& prices) {
          int n = prices.size();
          // max price after ith index
          int maxAfterIth = prices[n - 1];

          int maxProfit = 0;
          for (int i = n - 2; i >= 0; i--) {
              maxProfit = max(maxProfit, maxAfterIth - prices[i]);
              maxAfterIth = max(maxAfterIth, prices[i]);
          }
          return maxProfit ;
      }
  };
```

### 2. Maintain minPrice and maxProfit array till ith index

    Time Complexity: O(N)
    Space Complexity: O(N + N)

```c++
  class Solution {
  public:
      int maxProfit(vector<int>& prices) {
          int n = prices.size();
          vector<int> minPrice(n, 0);
          vector<int> maxProfit(n, 0);

          minPrice[0] = prices[0];
          maxProfit[0] = 0; // can't get profit on first day

          for (int i = 1; i < n; i++) {
              minPrice[i] = min(minPrice[i - 1], prices[i]);
              maxProfit[i] = max(maxProfit[i - 1], prices[i] - minPrice[i]);
          }
          return maxProfit[n - 1];
      }
  };
```
