# [Two Sum](https://leetcode.com/problems/two-sum/)

`Easy` `Array` `Hash Table`

## Approaches

### 1. For each element find its complement

    Time Complexity: O(N^2)
    Space Complexity: O(1)

### 2. Two pass Hash Table

    First Pass: Push values in the map with element as key and value as index
    Second Pass: For every element find the complement.
    Time Complexity: O(N)
    Space Complexity: O(N)

```c++
    class Solution {
    public:
        vector<int> twoSum(vector<int> &nums, int target) {
            unordered_map<int, int> hash;
            for (int i = 0; i < nums.size(); i++) {
                hash[nums[i]] = i;
            }
            for (int i = 0; i < nums.size(); i++) {
                int complement = target - nums[i];
                if (hash.find(complement) != hash.end() && hash[complement] != i) {
                    return {i, hash[complement]};
                }
            }
            return {};
        }
    };
```

### 3. Single pass Hash Table

    First find complement in Hash and then if not found push in Hash.

```c++
    class Solution {
    public:
        vector<int> twoSum(vector<int>& nums, int target) {
            unordered_map<int, int> mp;

            for (int i = 0; i < nums.size(); i++) {
                int remaining = target - nums[i];

                if (mp.find(remaining) != mp.end()) {
                    return {i, mp[remaining]};
                }
                mp[nums[i]] = i;
            }

            return {};
        }
    };

```
