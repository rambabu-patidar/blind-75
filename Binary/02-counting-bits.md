# [Counting Bits](https://leetcode.com/problems/counting-bits/description/)

`Easy` `Bit Manipulation` `Dynamic Programming`

## Approaches

### 1. Use [Count Bits](./01-number-of-1-bits.md) problem

    Time Complexity: O(nlog(n))
    Space Complexity: O(1)

```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> bitCount(n + 1);

        for (int i = 0; i <= n ; i++) {
            int currN = i;
            int count = 0;
            while (currN > 0) {
                currN &= (currN - 1);
                count++;
            }
            bitCount[i] = count;
        }

        // Time complexity : O(nlogn);
        // space complexity: O(1) {if not considered sent vector a extra space}
        return bitCount;
    }
};
```

### 2. Use STL

    Time Complexity: O(Nlog(N))
    Space Complexity: O(1)

```c++
  class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> bitCount(n + 1);

        for (int i = 0; i <= n ; i++) {
            bitCount[i] = __builtin_popcount(i);
        }
        return bitCount;
    }
};
```

### 2. Use STL

    Time Complexity: O(Nlog(N))
    Space Complexity: O(1)

```c++
  class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> bitCount(n + 1);

        for (int i = 0; i <= n ; i++) {
            bitCount[i] = __builtin_popcount(i);
        }
        return bitCount;
    }
};
```

### 3. Dynamic Programming (Tabulation approach)

If we half the current number and get a reminder 1 then we know that one extra bit needs to be added in the number Otherwise no need to add extra bit.

    Time Complexity: O(N)
    Space Complexity: O(N)

```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> bitCount(n + 1);

        bitCount[0] = 0;
        for (int i = 1; i <= n ; i++) {
            int currN = i;
            // if (currN & 1) {
            //     bitCount[currN] = bitCount[currN / 2] + 1;
            // }
            // else {
            //     bitCount[currN] = bitCount[currN / 2];
            // }

            bitCount[i] = (bitCount[i >> 1]) + (i & 1);
        }
        return bitCount;
    }
};
```
