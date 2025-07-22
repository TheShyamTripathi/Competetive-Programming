## 📘 Problem Statement

**Problem**:
You are given an array of integers `arr` of size `n`. A **Tribonacci number** is defined by the recurrence:

```
T(0) = 0, T(1) = 1, T(2) = 1  
T(n) = T(n-1) + T(n-2) + T(n-3) for n > 2
```

Generate all Tribonacci numbers up to `1e5`.

Your task is to **count the number of contiguous subarrays** where **every element** in the subarray is a **Tribonacci number**.

Since the number of subarrays can be large, return the result modulo **10⁹ + 7**.

---

## ✅ C++ Code Implementation

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

// Constants
const int MOD = 1e9 + 7;
const int MAX_VAL = 1e5;

/**
 * Generate all Tribonacci numbers up to MAX_VAL
 */
unordered_set<int> generateTribonacciSet() {
    unordered_set<int> tSet;
    int a = 0, b = 1, c = 1;
    tSet.insert(a);
    tSet.insert(b);
    tSet.insert(c);

    while (true) {
        int next = a + b + c;
        if (next > MAX_VAL) break;
        tSet.insert(next);
        a = b;
        b = c;
        c = next;
    }

    return tSet;
}

/**
 * Count the number of contiguous subarrays in which all elements are Tribonacci numbers
 */
int countTribonacciSubarrays(int n, const vector<int>& arr) {
    unordered_set<int> tribSet = generateTribonacciSet();
    long long count = 0;
    int left = 0;

    while (left < n) {
        // Skip non-Tribonacci numbers
        if (tribSet.count(arr[left]) == 0) {
            left++;
            continue;
        }

        // Find the right end of the current valid segment
        int right = left;
        while (right < n && tribSet.count(arr[right])) {
            right++;
        }

        // Length of current valid segment
        int len = right - left;

        // Count of subarrays = len * (len + 1) / 2
        count = (count + (1LL * len * (len + 1)) / 2) % MOD;

        // Move to next segment
        left = right;
    }

    return count;
}

/**
 * Main function
 */
int main() {
    int n;
    cin >> n;

    vector<int> arr(n);
    for (int& x : arr) cin >> x;

    int result = countTribonacciSubarrays(n, arr);
    cout << result << endl;

    return 0;
}
```

---

## 🧪 Example

### Input:

```
8
0 1 1 2 5 4 7 13
```

### Output:

```
16
```

### Explanation:

* Tribonacci numbers ≤ 13: {0, 1, 1, 2, 4, 7, 13}
* Valid segments:

  * `[0, 1, 1, 2]` → 4 elements → 4×5/2 = 10 subarrays
  * `[4, 7, 13]` → 3 elements → 3×4/2 = 6 subarrays
* Total: 10 + 6 = **16**





## 📘 Leetcode 1695: Maximum Erasure Value

### 🔗 Link:

[Leetcode Problem 1695 - Maximum Erasure Value](https://leetcode.com/problems/maximum-erasure-value/)

---

### 📝 Problem Statement:

You are given an array of positive integers `nums` and want to erase a subarray (contiguous elements) such that all elements are **unique**.

Return the **maximum sum** of elements in such a subarray.

---

### 🔍 Example:

**Input**:
`nums = [4,2,4,5,6]`
**Output**:
`17`
**Explanation**: The optimal subarray is `[2,4,5,6]`, with a sum of `2+4+5+6 = 17`.

---

### ✅ Constraints:

* `1 <= nums.length <= 10^5`
* `1 <= nums[i] <= 10^4`

---

### 🧠 Approach:

We use the **sliding window technique** to maintain a window `[left, right]` that always contains **unique elements**:

* Expand the window by moving `right` and add `nums[right]` to the current sum.
* If `nums[right]` already exists in the window, shrink the window from `left` until `nums[right]` becomes unique.
* Track the **maximum sum** of all valid windows.

---

### ✅ C++ Solution (with Comments):

```cpp
class Solution {
public:
    int maximumUniqueSubarray(vector<int>& nums) {
        unordered_map<int, int> freq; // To track frequency of elements in the current window
        int left = 0, curr_sum = 0, max_sum = 0;

        // Traverse the array using right pointer
        for (int right = 0; right < nums.size(); ++right) {
            int num = nums[right];
            freq[num]++;
            curr_sum += num;

            // If we see a duplicate, shrink the window from the left
            while (freq[num] > 1) {
                freq[nums[left]]--;
                curr_sum -= nums[left];
                left++;
            }

            // Update maximum sum with current valid window
            max_sum = max(max_sum, curr_sum);
        }

        return max_sum;
    }
};
```

---

### ⏱️ Time & Space Complexity:

* **Time Complexity**: `O(n)`
  Each element is inserted and removed at most once in the sliding window.
* **Space Complexity**: `O(n)`
  For storing frequencies of elements in the hashmap.

---


