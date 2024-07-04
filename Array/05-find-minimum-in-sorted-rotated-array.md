# [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

`Medium` `Array` `Binary Search`

## Key Points

- If the array is rotated in way that `rotation % n == 0` then just return the first element
- If size is one then also return that element
- Otherwise if `rotation % n != 0` then we definitely know that their is a peak in array before which array is increasing and also after which array is increasing.
- i.e. their is only one place where `nums[i - 1] > nums[i]`.

## Approaches

### 1. Use Binary search to catch the peak

    Time Complexity: O(log(N))
    Space Complexity: O(1)

```c++

class Solution {
public:
    int findMin(vector<int>& nums) {
        int n = nums.size();

        // If after rotation the array is sorted or array has 1 size
        if (nums[0] <= nums[n - 1]) {
            return nums[0];
        }

        // we need to find the pivot element(after which array again start increasing)

        int start = 0;
        int end = n - 1;

        // Now we know that array is rotated such that their must be a peak
        // so it must get caught in this loop.
        while (start <= end) {

            int mid = end - (end - start) / 2;

            if (nums[mid] < nums[mid - 1]) {
                return nums[mid];
            }else if (nums[mid] > nums[mid + 1]) {
                return nums[mid + 1];
            }else if (nums[mid] > nums[start]) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return -1;
    }
};
```
