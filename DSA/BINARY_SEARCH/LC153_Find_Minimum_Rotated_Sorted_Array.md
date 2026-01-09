# LeetCode 153: Find Minimum in Rotated Sorted Array

## Problem Summary

You are given a **rotated sorted array** with **unique elements**.
Your task is to find the **minimum element** in **O(log n)** time.

Example:

* `[4,5,6,7,0,1,2]` → `0`
* `[3,4,5,1,2]` → `1`

---

## Key Observation (Very Important)

A rotated sorted array looks like:

```
Left Sorted Part | Minimum | Right Sorted Part
```

Only **one place** breaks the sorted order — the **minimum element**.

Binary Search helps us decide **which side the minimum lies on**.

---

## Core Idea (Understand This Clearly)

We compare:

```
nums[mid] vs nums[r]
```

### Case 1: nums[mid] > nums[r]

* This means the **minimum is on the right side** of `mid`
* Because right side contains the rotation point

➡ Move left pointer:

```
l = mid + 1
```

### Case 2: nums[mid] <= nums[r]

* This means **mid could be the minimum**, or minimum lies on the **left side**
* We **cannot discard mid**

➡ Move right pointer:

```
r = mid
```

---

## Why `l < r` and NOT `l <= r` ❗

This is the **most important interview concept**.

### Rule of Thumb 🧠

| Situation                                   | Use      |
| ------------------------------------------- | -------- |
| Searching for an **index**                  | `l <= r` |
| Searching for a **minimum / maximum value** | `l < r`  |

---

### Why `l < r` Works Here

* We are **shrinking the search space** until **one element remains**
* That last element **must be the minimum**
* Loop stops naturally when `l == r`

If we used `l <= r`:

* We do `r = mid` (not `mid - 1`)
* This can cause **infinite loop**

---

## Key Difference Explained Simply

### `l <= r`

* Used when:

  * You want to **check every possible mid**
  * You are **returning an index**
* You usually do:

```
r = mid - 1
l = mid + 1
```

### `l < r`

* Used when:

  * You want to **converge to one answer**
  * You are **not eliminating mid completely**
* You usually do:

```
r = mid
l = mid + 1
```

---

## C++ Implementation

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int l = 0;
        int r = nums.size() - 1;

        // l < r ensures we stop when one element remains
        while (l < r) {
            int mid = l + (r - l) / 2;

            if (nums[mid] > nums[r]) {
                // Minimum is in right half
                l = mid + 1;
            } else {
                // Mid could be the minimum
                r = mid;
            }
        }

        // l == r pointing to minimum
        return nums[l];
    }
};
```

---

## Short Memory Tip 🧠 (For Interviews)

> "Compare mid with right — if mid is bigger, minimum is on the right"

or even shorter:

> "mid > right → go right"

---

## Common Interview Mistakes

* ❌ Using `l <= r` and getting infinite loop
* ❌ Doing `r = mid - 1` (you may lose the minimum)
* ❌ Comparing with `nums[l]` instead of `nums[r]`

---

## Time & Space Complexity

* **Time:** `O(log n)`
* **Space:** `O(1)`

---

## When You See This Pattern Again

Use this logic for:

* Find minimum in rotated array
* Peak finding problems
* Binary search on **answer space**

---

✅ Ready to paste into GitHub as `LC153_Find_Minimum_Rotated_Sorted_Array.md`
