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


