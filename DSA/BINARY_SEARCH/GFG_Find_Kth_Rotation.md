# GFG: Find Kth Rotation (Index of Minimum Element)

This problem is a **direct application of binary search on a rotated sorted array**.

---

## Problem Summary

You are given a **rotated sorted array with distinct elements**.

Each right rotation shifts the array by 1 position.
Your task is to **find how many times the array was rotated**.

---

## Key Insight (Most Important)

👉 **The number of rotations = index of the minimum element**

Why?

* Rotation breaks the sorted array at the **minimum element**
* Everything before the minimum was originally after it

Example:

```
Original: [1, 2, 3, 4, 5]
Rotated:  [3, 4, 5, 1, 2]
                   ↑
            index = 3 → rotated 3 times
```

---

## Core Binary Search Idea

We want to find the **minimum element index** using binary search.

### Why compare with the rightmost element?

For an element to be the **minimum**:

* All elements on its **right side must be greater**

So we compare:

```
arr[mid] with arr[right]
```

---

## Case Analysis (Understand This Clearly)

### Case 1: `arr[mid] < arr[r]`

* Right half is **sorted**
* `mid` **can be the minimum**
* So we **keep mid** and move left

```
r = mid
```

---

### Case 2: `arr[mid] > arr[r]`

* Minimum lies in the **right half**
* `mid` **cannot be minimum**

```
l = mid + 1
```

---

## Why `l < r` and NOT `l <= r`

* We are **converging to one index**
* We never discard `mid` blindly
* Loop stops naturally when `l == r`

At that point:

```
l == r == index of minimum
```

---

## C++ Code (Given Approach)

```cpp
class Solution {
  public:
    int findKRotation(vector<int> &arr) {
        int n = arr.size();
        int l = 0;
        int r = n - 1;
        
        while (l < r) {
            int mid = l + (r - l) / 2;
            
            if (arr[mid] < arr[r]) {
                // Right part sorted, mid can be minimum
                r = mid;
            } else {
                // Minimum lies on the right side
                l = mid + 1;
            }
        }
        return l; // index of minimum = number of rotations
    }
};
```

---

## How to Think Fast in Interviews 🧠

### Mental Checklist

1. Rotated sorted array?
2. Asked about rotations?
3. Rotations = position of minimum
4. Minimum → compare with **right**

---

## Short Memory Trick 🧠

> **"Rotation count = index of minimum"**

and

> **"Minimum checks the right side"**

---

## Time & Space Complexity

* **Time:** `O(log n)`
* **Space:** `O(1)`

---

## Where Else This Logic Is Used

This exact logic appears in:

* **LeetCode 153** – Find Minimum in Rotated Sorted Array
* **LeetCode 154** – With duplicates
* **Finding rotation count** problems
* **Search in rotated array** (LC 33)

Once you master this, **all rotated array problems become easy**.

---

## Interview-Ready One-Liner 💬

> "The number of rotations in a rotated sorted array is equal to the index of the minimum element, which can be found using binary search by comparing mid with the rightmost element."

---

✅ Ready to paste into GitHub as `GFG_Find_Kth_Rotation.md`
