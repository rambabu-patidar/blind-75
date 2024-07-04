# [Tree Sum](https://leetcode.com/problems/3sum/description/)

`Medium` `Array` `Sorting` `Two Pointer` `Hash Table`

## Key Points

- Fix one number and problem gets converted to two sum.
- For unique triplets use set of vector

## Approaches

### 1. Fix one number x and apply two sum via Hash Table

    Time Complexity: O(N*N)

    NOTE: couldn't pass last 3 cases. runtime error

```c++

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {

        // for every element in the nums we will use two sum question leaving the curr element.

        // we store the triplet in sorted order in set so to get unique triplets
        set<vector<int>> tripletSet;

        for (int i = 0; i < nums.size(); i++) {
            // nums[i] + a + b = 0
            // nums[i] = -(a + b)
            int target = -1 * nums[i];

            unordered_map<int, int> mapIdx;
            for (int j = i + 1; j < nums.size(); j++) {
                int subTarget = target - nums[j];
                if (mapIdx.find(subTarget) != mapIdx.end()) {
                    vector<int> triplet = {nums[i], nums[j], nums[mapIdx[subTarget]]};
                    // sorting will be constant as size is 3 always
                    sort(triplet.begin(), triplet.end());
                    tripletSet.insert(triplet);
                }

                mapIdx[nums[j]] = j;
            }
        }

        // put all element of set in vector
        vector<vector<int>> ans;
        auto it = tripletSet.begin();
        while (it != tripletSet.end()) {
            ans.push_back(*it);
            it++;
        }
        return ans;
    }
};
```

### 2. Fix one number x and apply two sum via two pointers

    we need to sort the array first

    Time Complexity: O(N \* N)
    Space Complexity: Possible triplets

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        // for every element in the nums we will use two sum question leaving the curr element.

        // we store the triplet in sorted order in set so to get unique triplets
        set<vector<int>> tripletSet;

        sort(nums.begin(), nums.end());
        for (int i = 0; i < n; i++) {
            // nums[i] + a + b = 0
            // nums[i] = -(a + b)
            int target = -1 * nums[i];

            int j = i + 1;
            int k = n - 1;

            while (j < k) {
                int sum = nums[j] + nums[k];
                if (sum == target) {
                    tripletSet.insert({nums[i], nums[j], nums[k]});
                    j++; k--;
                } else if (sum < target) {
                    j++;
                } else {
                    k--;
                }
            }
        }

        // put all element of set in vector
        vector<vector<int>> ans;
        auto it = tripletSet.begin();
        while (it != tripletSet.end()) {
            ans.push_back(*it);
            it++;
        }
        return ans;
    }
};
```
