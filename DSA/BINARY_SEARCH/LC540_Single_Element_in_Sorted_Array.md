# LeetCode 540: Single Element in a Sorted Array

## Problem Summary

You are given a **sorted array** where:

* Every element appears **exactly twice**
* Except **one element**, which appears **only once**

Your task is to find that **single element** in **O(log n)** time and **O(1)** space.

Example:

```
Input:  [1,1,2,3,3,4,4,8,8]
Output: 2
```

---

## Key Observation (Very Important)

In a normal situation (before the single element):

* Pairs start at **even index**

After the single element:

* Pair pattern **breaks**
* Pairs start at **odd index**

This pattern change helps us apply **binary search**.

---

## How to Think About the Solution (Step-by-Step)

### Step 1: Understand the pairing rule

If the array had **no single element**, indices would look like:

```
index: 0 1 | 2 3 | 4 5 | 6 7
value: a a | b b | c c | d d
```

Now when one element appears once, everything **after it shifts by one index**.

---

### Step 2: Use Binary Search on Index

We check `mid` and compare it with its pair:

* If `mid` is **even** → compare with `mid + 1`
* If `mid` is **odd** → compare with `mid - 1`

---

### Step 3: Decide which side to move

* If the pair is **valid** → single element is on the **right side**
* If the pair is **broken** → single element is on the **left side (including mid)**

---

## Why `l < r` and NOT `l <= r`

* We are **converging to one index**
* We never discard `mid` blindly
* Loop ends when `l == r`, pointing to the single element

---

## C++ Implementation

```cpp
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int l = 0, r = nums.size() - 1;

        while (l < r) {
            int mid = l + (r - l) / 2;

            // make mid even
            if (mid % 2 == 1) mid--;

            if (nums[mid] == nums[mid + 1]) {
                // correct pair, single element is on right
                l = mid + 2;
            } else {
                // broken pair, single element is on left
                r = mid;
            }
        }
        return nums[l];
    }
};
```

---

## Java Implementation (Simple & Clean)

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int l = 0;
        int r = nums.length - 1;

        while (l < r) {
            int mid = l + (r - l) / 2;

            // force mid to be even
            if (mid % 2 == 1) {
                mid--;
            }

            if (nums[mid] == nums[mid + 1]) {
                // correct pair
                l = mid + 2;
            } else {
                // broken pair
                r = mid;
            }
        }
        return nums[l];
    }
}
```

---

## Short Memory Trick 🧠 (Must Remember)

> "Before the single element → pairs start at even index"

or even shorter:

> "Fix mid to even, check next"

---

## Time & Space Complexity

* **Time:** `O(log n)`
* **Space:** `O(1)`

---

## Common Interview Mistakes

* ❌ Using linear scan (O(n))
* ❌ Forgetting to make `mid` even
* ❌ Using `l <= r` and getting stuck

---

## When You See This Pattern Again

This idea also appears in:

* Pair-based binary search problems
* Index parity based problems

---

✅ Ready to paste into GitHub as `LC540_Single_Element_in_Sorted_Array.md`
