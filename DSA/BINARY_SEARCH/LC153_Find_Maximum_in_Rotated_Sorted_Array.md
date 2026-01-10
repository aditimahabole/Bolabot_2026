# Find Maximum Element in a Rotated Sorted Array

This note is a **follow-up of LeetCode 153 (Find Minimum in Rotated Sorted Array)** and explains **how to think and find the maximum element** using binary search.

---

## Core Understanding (Very Important)

A rotated sorted array always looks like this:

```
[ larger values ... MAX ] [ MIN ... smaller values ]
```

* The array is originally sorted in ascending order
* Rotation breaks it at the **minimum element**
* The **maximum element is always just before the minimum**

---

## Why We Compare with RIGHT for Minimum

When finding the **minimum element**:

* A minimum element must have **all elements on its right side greater than or equal to it**
* That is why we compare:

```
nums[mid] with nums[right]
```

### Logic

* If `nums[mid] > nums[right]`

  * Minimum **cannot** be at `mid` or left of it
  * Minimum lies on the **right side**
* Else

  * `mid` **can be the minimum**
  * We move **leftward**

➡ We always shrink towards the minimum.

---

## How This Changes for Maximum Element

For an element to be the **maximum**:

* All elements on its **left side must be smaller than or equal to it**

So instead of checking the **right side**, we now check the **left side**.

That means we compare:

```
nums[mid] with nums[left]
```

---

## Two Clean Ways to Find Maximum

---

## Method 1: Find Minimum First, Then Get Maximum (Recommended)

### Idea

1. Find index of **minimum element** using standard binary search
2. The **maximum element is just before it**

### Formula

```
maxIndex = (minIndex - 1 + n) % n
```

### Java Code (Simple)

```java
class Solution {
    public int findMax(int[] nums) {
        int n = nums.length;
        int l = 0, r = n - 1;

        // Step 1: Find minimum index
        while (l < r) {
            int mid = l + (r - l) / 2;

            if (nums[mid] > nums[r]) {
                l = mid + 1;
            } else {
                r = mid;
            }
        }

        int minIndex = l;
        int maxIndex = (minIndex - 1 + n) % n;
        return nums[maxIndex];
    }
}
```

---

## Method 2: Direct Binary Search for Maximum

### Idea

* Since maximum needs **smaller elements on its left**
* We compare with `nums[left]`

### Logic

* If `nums[mid] >= nums[left]`

  * Left side is sorted
  * Maximum can be at `mid` or on the right
* Else

  * Maximum lies on the **left side**

---

### Java Code (Direct Approach)

```java
class Solution {
    public int findMax(int[] nums) {
        int l = 0, r = nums.length - 1;

        while (l < r) {
            int mid = l + (r - l + 1) / 2; // right biased

            if (nums[mid] >= nums[l]) {
                l = mid;
            } else {
                r = mid - 1;
            }
        }
        return nums[l];
    }
}
```

---

## How to Think Fast in Interviews 🧠

### Key Mental Rule

| Goal         | Compare With | Reason                                  |
| ------------ | ------------ | --------------------------------------- |
| Find Minimum | Right index  | Minimum needs greater elements on right |
| Find Maximum | Left index   | Maximum needs smaller elements on left  |

---

## Ultra-Short Memory Tricks

> **"Minimum checks right, Maximum checks left"**

and

> **"Max is always just before Min"**

---

## Time & Space Complexity

* **Time:** `O(log n)`
* **Space:** `O(1)`

---

## Interview-Ready Closing Line 💬

> "In a rotated sorted array, the maximum element is always just before the minimum. Since the minimum is found using right-side comparison, the maximum naturally follows from it or can be found by left-side comparison."

---

✅ Ready to paste into GitHub as `Find_Maximum_in_Rotated_Sorted_Array.md`
