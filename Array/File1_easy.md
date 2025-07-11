# Two Sum

**Problem Link**: [1. LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)  
**Difficulty**: Easy  
**Tags**: Array, Hash Table, Brute Force

---

## 🧠 Problem Statement

Given an array of integers `nums` and an integer `target`, return **indices** of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

---
## Code
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
       int n = nums.size();        
        for(int i = 0; i<n-1; i++){
            for(int j = i+1; j<n; j++){
                if(nums[i] + nums[j] == target){
                    return {i, j};
                    
                }
            }
        }

        return {0};
    }
};

```
## 🔍 Example

### Input:
```cpp
nums = [2, 7, 11, 15], target = 9

