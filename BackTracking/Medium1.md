
## 📝 Problem Note: Can Alice Share Chocolates Equally?

### 🔒 **Problem Statement**

Alice’s mom bought `n` bags of chocolates, numbered from 1 to `n`. The `i-th` bag contains `ai` chocolates.
Alice wants to share **some bags** with Bob such that **both of them get the same number of chocolates** in total.

> ❗ **Important Constraint**:
> The chocolates **inside a bag cannot be divided**. A bag is either **given as a whole** or not at all.

You are to determine **if it's possible to divide** the bags into **two groups** such that **both groups have an equal sum of chocolates**.

---

### 📥 Input Format

* First line: an integer `n` — number of bags.
* Second line: `n` space-separated integers representing chocolates in each bag.

### 📤 Output Format

* Print `"YES"` if it's possible to divide the chocolate bags into two groups with equal sum.
* Print `"NO"` otherwise.

---

### 🔒 Constraints

* `1 ≤ n ≤ 500`
* `1 ≤ ai ≤ 100` (number of chocolates in each bag)

---

### 📘 Sample Testcase 0

**Input**

```
4
1 2 3 3
```

**Output**

```
NO
```

**Explanation**:
Total chocolates = 9. Since the total is **odd**, it cannot be split equally → output is **NO**.

---

### 📗 Sample Testcase 1

**Input**

```
4
1 2 3 4
```

**Output**

```
YES
```

**Explanation**:
Total chocolates = 10
One valid split:

* Alice: 1, 4 → total = 5
* Bob: 2, 3 → total = 5
  ✅ Equal chocolates possible.

---

### 🧠 Algorithm Used: **Subset Sum using Backtracking**

This is a classic **Subset Sum Problem**, where we check:

* Can we pick a subset of the given chocolate bag values that adds up to **half of the total sum**?

#### ✔ Steps:

1. Calculate the total sum of all chocolates.
2. If the sum is odd → immediately return `"NO"`.
3. Else, target = `totalSum / 2`.
4. Use a recursive function (`isSubsetSum`) to check if a subset with sum = target exists:

   * At each step, **choose** or **skip** the current bag.
   * If any valid combination gives exact target sum → return `"YES"`.

#### 🧮 Time Complexity:

* Worst-case: `O(2^n)` due to recursion, but manageable for `n ≤ 500` due to small values and early pruning.

> ✅ Optimization Possible: Use **Dynamic Programming (DP)** to improve to `O(n × sum)`.

---

### ✅ Final Working Code

```cpp
#include <iostream>
#include <vector>
#include <numeric>
using namespace std;

bool isSubsetSum(int start, vector<int>& chocolates, int target){
    if(target == 0) return true;
    if(start == chocolates.size() || target < 0) return false;

    // Choice 1: Take chocolates[start]
    if(isSubsetSum(start + 1, chocolates, target - chocolates[start])) return true;

    // Choice 2: Skip chocolates[start]
    return isSubsetSum(start + 1, chocolates, target);
}

string can_partition_chocolates(int n, vector<int>& chocolates) {
    int chocolatesSum = accumulate(chocolates.begin(), chocolates.end(), 0);
    if(chocolatesSum % 2 != 0) return "NO";

    int target = chocolatesSum / 2;

    if(isSubsetSum(0, chocolates, target))
        return "YES";
    else
        return "NO";
}

int main() {
    int n;
    cin >> n;
    vector<int> chocolates(n);
    for (int i = 0; i < n; ++i) {
        cin >> chocolates[i];
    }
    cout << can_partition_chocolates(n, chocolates) << endl;
    return 0;
}
```

---

### 🔍 Summary

| Element         | Description                                  |
| --------------- | -------------------------------------------- |
| Problem Type    | Subset Sum / Partition Problem               |
| Algorithm Used  | Backtracking with "Take / Not Take" decision |
| Time Complexity | Exponential `O(2^n)` (can be optimized)      |
| Optimization    | Possible via Memoization or Bottom-Up DP     |
| Constraints Fit | Yes (`n ≤ 500`, `ai ≤ 100`)                  |


