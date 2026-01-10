# LeetCode 33: Search in Rotated Sorted Array

This problem combines **rotation logic + binary search**. Once you understand the pattern, it becomes very straightforward.

---

## Problem Summary

You are given a **rotated sorted array with distinct elements** and a `target`.

You need to return the **index of the target** if present, otherwise `-1`.

Example:

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

---

## Core Idea (Very Important)

A rotated sorted array looks like:

```
[ sorted part ] [ sorted part ]
```

The rotation happens at the **minimum element**.

👉 If we find the **index of the minimum element (pivot)**:

* Left side of pivot is sorted
* Right side of pivot is sorted

Then we can apply **normal binary search** on both parts.

---

## Step-by-Step Approach

### Step 1: Find the Pivot (Index of Minimum Element)

Why?

* The pivot divides the array into **two sorted halves**

### How do we find the pivot?

We use binary search and compare with the **rightmost element**.

#### Why compare with right?

* For an element to be **minimum**, all elements on its **right must be greater**

---

### Pivot Finding Logic

* If `nums[mid] < nums[right]`

  * Right side is sorted
  * `mid` **can be the minimum**
  * Move left: `r = mid`

* Else

  * Minimum lies on the right side
  * Move right: `l = mid + 1`

At the end:

```
l == r == pivot index
```

---

## Step 2: Binary Search in Sorted Ranges

Once pivot is known:

* Search in range `[0 ... pivot-1]`
* If not found, search in `[pivot ... n-1]`

Each range is **sorted**, so normal binary search applies.

---

## C++ Code

```cpp
class Solution {
public:
    int findPivot(vector<int>& nums, int n) {
        int l = 0, r = n - 1;

        while (l < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] < nums[r]) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }

    int findInRange(int start, int end, vector<int>& nums, int target) {
        int l = start, r = end;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) l = mid + 1;
            else r = mid - 1;
        }
        return -1;
    }

    int search(vector<int>& nums, int target) {
        int n = nums.size();
        int pivot = findPivot(nums, n);

        int pos = findInRange(0, pivot - 1, nums, target);
        if (pos != -1) return pos;

        return findInRange(pivot, n - 1, nums, target);
    }
};
```

---

## Java Code (Simple & Clean)

```java
class Solution {
    private int findPivot(int[] nums) {
        int l = 0, r = nums.length - 1;

        while (l < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] < nums[r]) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }

    private int binarySearch(int l, int r, int[] nums, int target) {
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) l = mid + 1;
            else r = mid - 1;
        }
        return -1;
    }

    public int search(int[] nums, int target) {
        int pivot = findPivot(nums);

        int pos = binarySearch(0, pivot - 1, nums, target);
        if (pos != -1) return pos;

        return binarySearch(pivot, nums.length - 1, nums, target);
    }
}
```

---

## Short Memory Trick 🧠 (Must Remember)

> **"Rotation breaks the array at the minimum element"**

So:

1. Find minimum (pivot)
2. Binary search on both sorted halves

---

## Time & Space Complexity

* **Time:** `O(log n)`
* **Space:** `O(1)`

---

## Where Else This Logic Is Used

This exact logic applies to:

* **LC 153** – Find Minimum in Rotated Sorted Array
* **GFG Find Kth Rotation**
* Variants of rotated array search problems

---

## Interview-Ready One-Liner 💬

> "I first find the pivot (minimum element) to split the rotated array into two sorted parts, then apply binary search on each part."

---

✅ Ready to paste into GitHub as `LC33_Search_in_Rotated_Sorted_Array.md`
