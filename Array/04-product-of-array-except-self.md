# [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)

`Medium` `Array` `Prefix & Suffix Product`

## Approaches

### 1. Find Prefix Product and Suffix Product in separate arrays

    Time Complexity: O(N)
    Space Complexity: O(N + N)

```c++
  class Solution {
    public:
      vector<int> productExceptSelf(vector<int>& nums) {
          int n = nums.size();

          // to store the product from [0, i) at i th position
          vector<int> prefixProduct(n, 1);

          // to store the product from (i, n - 1] index
          vector<int> suffixProduct(n, 1);

          for (int i = 1; i < n; i++) {
              prefixProduct[i] = prefixProduct[i - 1] * nums[i - 1];
              suffixProduct[n - i - 1] = suffixProduct[n - i] * nums[n - i];
          }

          vector<int> answer(n, 1);
          for (int i = 0; i < n; i++) {
              answer[i] = prefixProduct[i] * suffixProduct[i];
          }
          return answer;
      }
    };
```

### 2. Use the answer array itself to store the prefix product and a variable to store suffix product

    Time Complexity: O(N + N)
    Space Complexity: O(1) [answer array is not considered as extra space as per question]

```c++
    class Solution {
    public:
        vector<int> productExceptSelf(vector<int>& nums) {
            int n = nums.size();

            // now lets do the work of prefix and suffix product in the answer array itself to not use extra space.
            vector<int> answer(n, 1);

            // First pass: calculate prefix products and store in answer
            for (int i = 1; i < n; i++) {
                answer[i] = answer[i - 1] * nums[i - 1];
            }

            // Second pass: calculate suffix products and update answer
            int suffixProduct = 1;
            for (int i = n - 1; i >= 0; i--) {
                answer[i] = answer[i] * suffixProduct;
                suffixProduct *= nums[i];
            }
            return answer;
        }
    };
```
