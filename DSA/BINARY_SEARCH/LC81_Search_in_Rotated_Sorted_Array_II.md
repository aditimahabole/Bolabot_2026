# LeetCode 81: Search in Rotated Sorted Array II

This problem is an **extension of LeetCode 33**, with **one extra difficulty**:

👉 **Duplicates are allowed**.

Because of duplicates, some clean binary-search guarantees break, so we need to be a bit careful.

---

## Problem Summary

You are given a **rotated sorted array** that **may contain duplicates** and a `target`.

Return `true` if the target exists, otherwise `false`.

Example:

```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

---

## Which Pattern Does This Problem Belong To?

👉 **Binary Search on Rotated Sorted Array (with duplicates)**

This is the same pattern as:

* **LC 33** – without duplicates
* **LC 153 / GFG Kth Rotation** – finding pivot (minimum)

But duplicates force us to **add a duplicate-skipping step**.

---

## Core Idea (Simple Explanation)

A rotated sorted array always breaks at the **minimum element**.

If we can find the **pivot (index of minimum)**:

* Left side of pivot is sorted
* Right side of pivot is sorted

Then we can apply **normal binary search** on both halves.

The only issue here is:

> **Duplicates can hide the pivot**

So we must **skip duplicates** while finding the pivot.

---

## Step 1: Finding the Pivot (Minimum Element Index)

### Why pivot is needed?

* Pivot splits the array into **two sorted parts**

### Why duplicates cause a problem?

If:

```
nums[l] == nums[mid] == nums[r]
```

We cannot decide which side is sorted.

So we **shrink the search space** by skipping duplicates.

---

### Pivot Finding Logic

1. Skip duplicates from left and right
2. Compare `nums[mid]` with `nums[r]`

#### Case 1: `nums[mid] < nums[r]`

* Right side is sorted
* `mid` **can be the minimum**
* Move left

```
r = mid
```

#### Case 2: `nums[mid] > nums[r]`

* Minimum lies on the right side
* `mid` can never be minimum

```
l = mid + 1
```

At the end:

```
l == r == pivot index
```

---

## Step 2: Binary Search in Both Sorted Halves

Once pivot is known:

* Binary search in `[0 ... pivot-1]`
* If not found, binary search in `[pivot ... n-1]`

---

## C++ Code (Your Approach)

```cpp
class Solution {
public:
    int findPivot(vector<int>& nums , int n){
        int l = 0;
        int r = n-1;

        while(l < r){
            // skip duplicates from left and right
            while(l < r && nums[l] == nums[l+1]) l++;
            while(l < r && nums[r] == nums[r-1]) r--;

            int mid = l + (r - l) / 2;
            if(nums[mid] < nums[r]){
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return r; // l == r
    }

    bool binarySearch(int start, int end, vector<int>& nums, int target){
        while(start <= end){
            int mid = start + (end - start) / 2;
            if(nums[mid] == target) return true;
            else if(nums[mid] < target) start = mid + 1;
            else end = mid - 1;
        }
        return false;
    }

    bool search(vector<int>& nums, int target) {
        int n = nums.size();
        int pivot = findPivot(nums, n);

        if(binarySearch(0, pivot - 1, nums, target)) return true;
        return binarySearch(pivot, n - 1, nums, target);
    }
};
```

---

## Java Code (Simple, No Heavy Java)

```java
class Solution {
    private int findPivot(int[] nums) {
        int l = 0, r = nums.length - 1;

        while (l < r) {
            // skip duplicates
            while (l < r && nums[l] == nums[l + 1]) l++;
            while (l < r && nums[r] == nums[r - 1]) r--;

            int mid = l + (r - l) / 2;
            if (nums[mid] < nums[r]) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }

    private boolean binarySearch(int l, int r, int[] nums, int target) {
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) return true;
            else if (nums[mid] < target) l = mid + 1;
            else r = mid - 1;
        }
        return false;
    }

    public boolean search(int[] nums, int target) {
        int pivot = findPivot(nums);

        if (binarySearch(0, pivot - 1, nums, target)) return true;
        return binarySearch(pivot, nums.length - 1, nums, target);
    }
}
```

---

## Why Time Complexity Is Not Always O(log n)

Because of duplicates:

* In worst case (all elements same), we keep shrinking one-by-one

Worst case time:

```
O(n)
```

Best / Average case:

```
O(log n)
```

---

## Short Memory Trick 🧠

> **"Same as LC33, but duplicates hide the pivot — so skip them."**

or even shorter:

> **"Duplicates → shrink first, then binary search."**

---

## Where This Pattern Appears Again

* LC 33 – Rotated array (no duplicates)
* LC 81 – Rotated array (with duplicates)
* LC 153 / 154 – Find minimum (with & without duplicates)

If you understand this, **all rotated-array questions are covered**.

---

## Interview-Ready One-Liner 💬

> "This is a rotated sorted array with duplicates. I first find the pivot while skipping duplicates, then apply binary search on both sorted halves."

---

✅ Ready to paste into GitHub as `LC81_Search_in_Rotated_Sorted_Array_II.md`
