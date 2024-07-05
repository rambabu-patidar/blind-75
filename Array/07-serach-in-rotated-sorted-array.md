# [Search In Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

`Medium` `Array` `Binary Search`

## Key Points

- The question uses [Find minimum in rotated sorted array](05-find-minimum-in-sorted-rotated-array.md)
- This is little modification to that question such that we find peak idx(a peak idx is a element's idx where the maximum of array is found in rotated array)
- We do binary search in both left and right increasing sequences.
- We return -1 as Peak idx if the array is already sorted or it has a size of 1

## Approaches

### 1. Use Binary search to catch the peak idx and do Binaray search in both side of peak.

    Time Complexity: O(log(N))
    Space Complexity: O(1)

```c++
class Solution {
public:
    // find the peak index
    int findPeak(vector<int> &nums) {

        int n = nums.size();

        // if size is one or array is increasing
        if (n == 1 || nums[0] < nums[n - 1]) {
            return -1;
        }

        int l = 0;
        int r = n - 1;

        while (l <= r) {
            int mid = r - (r - l) / 2;

            if (mid - 1 >= 0 && nums[mid - 1] > nums[mid]) {
                return mid - 1;
            } else if (mid + 1 < n && nums[mid] > nums[mid + 1]) {
                return mid;
            } else if (nums[l] < nums[mid]) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return -1;
    }

    // standard binary search No magic here.
    int binarySearch(vector<int> &nums, int target, int l, int r) {
        while (l <= r) {
            int mid = r - (r - l) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return -1;
    }

    int search(vector<int>& nums, int target) {
        int n = nums.size();
        // if I am getting -1 as peak then just do the single binary search
        int peakIdx = findPeak(nums);

        if (peakIdx == -1) {
            // do binary search [0, n - 1]
            return binarySearch(nums, target, 0, n - 1);
        }

        // searching left increasing sequence [0, peakIdx]
        int targetIdx = binarySearch(nums, target, 0, peakIdx);
        if (targetIdx != -1) {
            return targetIdx;
        }

        // if now found we need to search in the right increasing sequence [peakIdx + 1, n - 1]
        return binarySearch(nums, target, peakIdx + 1, n - 1);
    }
};
```
