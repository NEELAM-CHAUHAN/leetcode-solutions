# Maximum Subarray With Equal Products

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

You are given an array of **positive** integers `nums`.

An array `arr` is called **product equivalent** if `prod(arr) == lcm(arr) * gcd(arr)`, where:

- prod(arr) is the product of all elements of arr.
- gcd(arr) is the GCD of all elements of arr.
- lcm(arr) is the LCM of all elements of arr.

Return the length of the **longest** **product equivalent** subarray of `nums`.

 

Original
C++
**Example 1:**

**Input:** nums = [1,2,1,2,1,1,1]

**Output:** 5

**Explanation:** 

The longest product equivalent subarray is `[1, 2, 1, 1, 1]`, where `prod([1, 2, 1, 1, 1]) = 2`, `gcd([1, 2, 1, 1, 1]) = 1`, and `lcm([1, 2, 1, 1, 1]) = 2`.

**Example 2:**

**Input:** nums = [2,3,4,5,6]

**Output:** 3

**Explanation:** 

The longest product equivalent subarray is `[3, 4, 5].`

**Example 3:**

**Input:** nums = [1,2,3,1,4,5,1]

**Output:** 5

 

**Constraints:**

- 2 <= nums.length <= 100
- 1 <= nums[i] <= 10

## Solution

**Language:** C++  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 28 MB (beats 73.31%)  
**Submitted:** 2026-11-24T18:11:25.632Z  

```cpp
class Solution {
    static constexpr int PRIMES[11][2] = {
        {-1, -1}, {-1, -1}, {0, -1}, {1, -1}, {0, -1},
        {2, -1},  {0, 1},   {3, -1}, {0, -1}, {1, -1}, {0, 2}
    };

public:
    int maxLength(vector<int>& nums) {
        int last[4] = {-1, -1, -1, -1}, ans = 2, left = 0;

        for (int right = 0; right < nums.size(); ++right) {
            for (int p : PRIMES[nums[right]]) {
                if (p != -1) {
                    left = max(left, last[p] + 1);
                    last[p] = right;
                }
            }
            ans = max(ans, right - left + 1);
        }

        return ans;
    }
};
```

---

[View on LeetCode](https://leetcode.com/problems/maximum-subarray-with-equal-products/)