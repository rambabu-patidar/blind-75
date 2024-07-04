# [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

`Easy` `Array` `Hash Table` `Sorting`

## Approaches

### 1. Maintain a frequency array

    Time Complexity: O(N)
    Space Complexity: O(N)

    NOTE: This is wrong intution as numbers can be negative and maintaing an array as hash table for negative number is unnessesary complicate our problem.

### 2. Sort the array

    sort the array and watch if two number occur consecutively
    Time Complexity: O(Nlog(N))
    Space Complexity: O(1)

### 3. Maintain frequency using Hash table (Two Pass)

    First Pass: Push the element in hash table and increment their count
    Second Pass: Iterate over hash table and see if you have element greater than 1 freq.
    Time Complexity: O(N)
    Space Complexity: O(N)

```c++
    class Solution {
    public:
        bool containsDuplicate(vector<int>& nums) {
            int n = nums.size();
            unordered_map<int, int> freqCount;

            for (int i = 0; i < n; i++) {
                freqCount[nums[i]]++;
            }

            unordered_map<int, int>::iterator it = freqCount.begin();
            while (it != freqCount.end()) {
                if (it->second > 1) {
                    return true;
                }
                it++;
            }
            return false;
        }
    };
```

### 4. Single pass Hash Table

    Increment the count in hash table and see if this increment made freq greater then 1

    Time Complexity: O(N)
    Space Complexity: O(N)

```c++
    class Solution {
    public:
        bool containsDuplicate(vector<int>& nums) {
            int n = nums.size();
            unordered_map<int, int> freqCount;

            for (int i = 0; i < n; i++) {
                freqCount[nums[i]]++;
                if (freqCount[nums[i]] > 1) {
                    return true;
                }
            }
            return false;
        }
    };

```
