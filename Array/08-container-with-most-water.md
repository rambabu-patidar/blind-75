# [Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)

`Medium` `Array` `Two Pointer`

## Key Points

- Standard two pointer problem where pointers start from both ends.

## Approaches

### 1. Use two pointer from both end and move closer removing the smaller height

    Time Complexity: O(N)
    Space Complexity: O(1)

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();

        int left = 0;
        int right = n - 1;

        int maxWater = INT_MIN;
        while (left < right) {
            maxWater = max(maxWater, min(height[left], height[right]) * (right - left));
            if (height[left] <= height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxWater;

    }
};
```
