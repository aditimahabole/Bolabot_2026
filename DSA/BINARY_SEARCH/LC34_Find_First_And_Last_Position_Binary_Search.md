# LeetCode 34: Find First and Last Position of Element in Sorted Array

## Problem Summary

Given a **sorted array** `nums` and a `target`, return the **first (leftmost)** and **last (rightmost)** index of `target`.
If `target` is not present, return `[-1, -1]`.

---

## Key Idea (Interview-Friendly)

* The array is **sorted** → use **Binary Search**.
* A normal binary search stops when it finds the element.
* Here, we need **boundaries**, so:

  * One binary search to find the **leftmost occurrence**
  * One binary search to find the **rightmost occurrence**

Each search runs in **O(log n)** → total **O(log n)**.

---

## Steps to Solve (Quick Revision)

### Step 1: Find Leftmost Index

* Initialize `answer = -1`
* If `nums[mid] == target`

  * Save `mid` as a possible answer
  * Move **left** (`r = mid - 1`) to find an earlier occurrence
* Else:

  * If `nums[mid] < target` → move right
  * Otherwise → move left

### Step 2: Find Rightmost Index

* Initialize `answer = -1`
* If `nums[mid] == target`

  * Save `mid` as a possible answer
  * Move **right** (`l = mid + 1`) to find a later occurrence
* Else:

  * If `nums[mid] < target` → move right
  * Otherwise → move left

### Step 3: Return Result

* `{leftMost, rightMost}`

---

## C++ Implementation

```cpp
class Solution {
public:
    int findLeftMost(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        int ans = -1;

        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) {
                ans = mid;       // possible answer
                r = mid - 1;     // search left
            } else if (nums[mid] < target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return ans;
    }

    int findRightMost(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        int ans = -1;

        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) {
                ans = mid;       // possible answer
                l = mid + 1;     // search right
            } else if (nums[mid] < target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return ans;
    }

    vector<int> searchRange(vector<int>& nums, int target) {
        return {findLeftMost(nums, target), findRightMost(nums, target)};
    }
};
```

---

## Java Implementation

```java
class Solution {
    private int findLeftMost(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        int ans = -1;

        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) {
                ans = mid;       // possible answer
                r = mid - 1;     // search left
            } else if (nums[mid] < target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return ans;
    }

    private int findRightMost(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        int ans = -1;

        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) {
                ans = mid;       // possible answer
                l = mid + 1;     // search right
            } else if (nums[mid] < target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return ans;
    }

    public int[] searchRange(int[] nums, int target) {
        return new int[] {
            findLeftMost(nums, target),
            findRightMost(nums, target)
        };
    }
}
```

---

## Common Interview Notes

* Always clarify **sorted array** → binary search
* Mention **two binary searches** explicitly
* Time Complexity: **O(log n)**
* Space Complexity: **O(1)**

---

## One-Line Memory Trick 🧠

> "If found → save index → keep searching towards the boundary"

---

