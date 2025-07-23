

## ✅ Problem Summary (LeetCode 1717):

Given a string `s` and two integers `x` and `y`, you can repeatedly remove the substrings `"ab"` and `"ba"` from `s`. Each time you remove `"ab"`, you gain `x` points; each time you remove `"ba"`, you gain `y` points.
Return the **maximum total score** you can obtain after performing these operations in any order.

---

### 🔑 Key Insight:

To maximize the total score:

* Always remove the **more profitable substring** first (`"ab"` if `x > y`, otherwise `"ba"`), to avoid blocking higher-value matches.
* Use a **stack-based approach** to simulate greedy pair removals in a single pass.

---

### ✅ Clean and Commented C++ Solution:

```cpp
class Solution {
public:
    int maximumGain(string s, int x, int y) {
        // Decide which substring to remove first based on higher score
        // Remove the higher value substring first for maximum gain
        if (x > y) {
            return calculateGain(s, "ab", x, "ba", y);
        } else {
            return calculateGain(s, "ba", y, "ab", x);
        }
    }

private:
    // Helper function to calculate total gain from removing sub1 first, then sub2
    int calculateGain(const string& s, const string& sub1, int val1,
                      const string& sub2, int val2) {
        int totalScore = 0;
        vector<char> stack1;

        // First pass: remove as many occurrences of sub1 as possible
        for (char c : s) {
            if (!stack1.empty() && stack1.back() == sub1[0] && c == sub1[1]) {
                stack1.pop_back();
                totalScore += val1;
            } else {
                stack1.push_back(c);
            }
        }

        // Second pass: remove as many occurrences of sub2 from the leftover string
        vector<char> stack2;
        for (char c : stack1) {
            if (!stack2.empty() && stack2.back() == sub2[0] && c == sub2[1]) {
                stack2.pop_back();
                totalScore += val2;
            } else {
                stack2.push_back(c);
            }
        }

        return totalScore;
    }
};
```

---

### 🧠 Why This Works:

* Using stacks ensures **efficient adjacent character matching and removal**.
* By always removing the more valuable pair first, we ensure the **greedy strategy maximizes the total score**.
* The order matters because certain substrings can overlap or block each other.

---

### 🕒 Time & Space Complexity:

* **Time:** O(n), where n is the length of string `s` — each character is visited at most twice.
* **Space:** O(n) for the stacks used to simulate removals.

---

