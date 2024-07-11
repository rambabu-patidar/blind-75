# [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/description/)

`Easy` `Bit Manipulation` `Divide and conquer`

## Key Points

- `n &= n - 1` operation in bit removes the rightmost set bit of number n
- This is also used where we want to find the position of rightmost set bit

## Approaches

### 1. Divide by 2 and record when you get reminder 1

    Time Complexity: O(log(n))
    Space Complexity: O(1)

```c++
class Solution {
public:

    int hammingWeightUtil(int n) {
        int count = 0;
        while (n > 0) {
            if (n & 1) {
                count++;
            }
            n /= 2;
            // n >>= 1; // this also removes the last bit and make number half
        }
        return count;
    }

    int hammingWeight(int n) {
        return hammingWeightUtil(n);
    }
};
```

### 2. Using more bit manipulation

    Time Complexity: O(log(N))
    Space Complexity: O(1)

```c++
   class Solution {
public:

    int hammingWeightUtil(int n) {
        int count = 0;
        while (n > 0) {
            // removes the right most set bit always.
            n &= (n - 1);
            count++;
        }
        return count;
    }

    int hammingWeight(int n) {
        return hammingWeightUtil(n);
    }
};
```
