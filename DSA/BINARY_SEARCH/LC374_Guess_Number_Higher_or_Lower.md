# LeetCode 374: Guess Number Higher or Lower

This is a **classic binary search problem** where the search space is **numbers**, not an array.

---

## Problem Summary

You are asked to guess a number picked between `1` and `n`.

You are given a helper API:

```text
guess(num)
- returns  0 if num == picked number
- returns -1 if num is higher than picked number
- returns  1 if num is lower than picked number
```

Your task is to find the picked number.

---

## Which Pattern Does This Belong To?

👉 **Binary Search on Answer Space**

* There is no array
* The answer lies in a **range [1 … n]**
* Feedback tells you whether to go **left or right**

This is the same thinking used in:

* Binary search on numbers
* Binary search on constraints

---

## Core Idea (Simple Explanation)

Even though there is no array, the problem behaves exactly like binary search:

* Search space = numbers from `1` to `n`
* `guess(mid)` tells you:

  * too high → move left
  * too low → move right

So we repeatedly cut the range into half.

---

## Step-by-Step Approach

### Step 1: Define Search Space

```
l = 1
r = n
```

### Step 2: Pick the Middle Number

```
mid = l + (r - l) / 2
```

### Step 3: Use guess(mid)

* If `guess(mid) == 0` → found the answer
* If `guess(mid) == -1` → mid is too large → move left
* If `guess(mid) == 1` → mid is too small → move right

Repeat until found.

---

## Why `l <= r` Is Used

* We are searching for an **exact value**
* We discard `mid` completely once checked
* Standard binary search condition applies

---

## C++ Code

```cpp
class Solution {
public:
    int guessNumber(int n) {
        int l = 1;
        int r = n;
        
        while (l <= r) {
            int mid = l + (r - l) / 2;
            int res = guess(mid);
            
            if (res == 0) return mid;
            else if (res == -1) r = mid - 1;
            else l = mid + 1;
        }
        return -1;
    }
};
```

---

## Java Code (Simple)

```java
public class Solution {
    public int guessNumber(int n) {
        int l = 1;
        int r = n;

        while (l <= r) {
            int mid = l + (r - l) / 2;
            int res = guess(mid);

            if (res == 0) return mid;
            else if (res == -1) r = mid - 1;
            else l = mid + 1;
        }
        return -1;
    }
}
```

---

## Short Memory Trick 🧠

> **"No array? Still binary search on numbers."**

or

> **"guess(mid) tells which half to remove."**

---

## Time & Space Complexity

* **Time:** `O(log n)`
* **Space:** `O(1)`

---

## Common Interview Mistakes

* ❌ Forgetting integer overflow protection (`l + (r-l)/2`)
* ❌ Using `l < r` instead of `l <= r`
* ❌ Treating it as linear guessing

---

## Where Else This Logic Appears

This exact thinking is reused in:

* Binary search on answer problems
* Capacity / minimum / maximum problems
* Games with feedback (higher / lower)

---

## Interview-Ready One-Liner 💬

> "This is binary search on the answer space from 1 to n, where the guess API tells us which half to discard."

---

✅ Ready to paste into GitHub as `LC374_Guess_Number_Higher_or_Lower.md`
