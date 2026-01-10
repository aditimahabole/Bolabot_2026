# LeetCode 74: Search a 2D Matrix

## Problem Summary

You are given an `m x n` matrix with these properties:

* Each row is **sorted in ascending order**
* The **first element of each row is greater than the last element of the previous row**

Task: Check if a given `target` exists in the matrix.

---

## Approach 1: Staircase Search (Top-Right Start)

### Idea

* Start from **top-right corner**
* From any cell:

  * If value is **greater than target** → move **left**
  * If value is **less than target** → move **down**

Why this works:

* Moving left decreases values
* Moving down increases values

### Time & Space

* **Time:** `O(m + n)`
* **Space:** `O(1)`

### C++ Code (Approach 1)

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();

        int i = 0;      // row
        int j = n - 1;  // column

        while (i < m && j >= 0) {
            if (matrix[i][j] == target) return true;
            else if (matrix[i][j] > target) j--;   // move left
            else i++;                               // move down
        }
        return false;
    }
};
```

### Java Code (Approach 1)

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;

        int i = 0;      // row
        int j = n - 1;  // column

        while (i < m && j >= 0) {
            if (matrix[i][j] == target) return true;
            else if (matrix[i][j] > target) j--;   // move left
            else i++;                               // move down
        }
        return false;
    }
}
```

---

## Approach 2: Binary Search (Treat Matrix as 1D Array) ⭐

### Core Idea

Because:

* Rows are sorted
* Last element of a row < first element of next row

➡ The entire matrix behaves like **one sorted 1D array**.

We apply **binary search** on indices `[0 .. m*n-1]`.

---

## How to Calculate Row & Column (VERY IMPORTANT)

Imagine flattening the matrix row-wise:

```
Index: 0 1 2 3 | 4 5 6 7 | 8 9 10 11
Matrix:
[ a b c d ]
[ e f g h ]
[ i j k l ]
```

Let:

* `n` = number of columns

### Formula to remember 🧠

```
row = index / n
col = index % n
```

### Why this works

* Every `n` elements, we move to a **new row** → division
* Remainder tells us **column position** → modulo

---

## C++ Code (Approach 2 – Binary Search)

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();

        int start = 0;
        int end = m * n - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;
            int r = mid / n;   // row
            int c = mid % n;   // column

            if (matrix[r][c] == target) return true;
            else if (matrix[r][c] < target) start = mid + 1;
            else end = mid - 1;
        }
        return false;
    }
};
```

---

## Java Code (Approach 2 – Binary Search)

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;

        int start = 0;
        int end = m * n - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;
            int r = mid / n;   // row
            int c = mid % n;   // column

            if (matrix[r][c] == target) return true;
            else if (matrix[r][c] < target) start = mid + 1;
            else end = mid - 1;
        }
        return false;
    }
}
```

---

## Short Memory Trick 🧠 (Must Remember)

> "Matrix is just a sorted array pretending to be 2D"

and

> "Divide for row, modulo for column"

---

## When to Use Which Approach?

| Situation                          | Approach         |
| ---------------------------------- | ---------------- |
| Want simplest logic                | Staircase search |
| Interview expects optimal solution | Binary search    |

---

## Complexity Comparison

| Approach      | Time        | Space |
| ------------- | ----------- | ----- |
| Staircase     | O(m + n)    | O(1)  |
| Binary Search | O(log(m*n)) | O(1)  |

---
# Time Complexity

Great question — this is **exactly** the kind of thing interviewers ask next.
Let’s make it **intuitive**, not textbook-heavy.

---

## Why Approach-1 (Staircase Search) is **O(m + n)**

### Setup

* Matrix size = `m x n`
* We start at **top-right corner**: `(row = 0, col = n-1)`

From **any cell**, we only do **one of two moves**:

| Comparison result | Move | What changes |
| ----------------- | ---- | ------------ |
| Current > target  | Left | `col--`      |
| Current < target  | Down | `row++`      |

---

## Key Insight (This is the secret)

👉 **We never move up or right.**
👉 Every step **removes one row or one column forever**.

---

## Maximum number of moves

### Row movement

* `row` starts at `0`
* Can increase **at most `m` times**
* After `row == m`, we exit

### Column movement

* `col` starts at `n-1`
* Can decrease **at most `n` times**
* After `col == -1`, we exit

---

## Total steps = row moves + column moves

```
Max steps = m (down moves) + n (left moves)
```

So:

```
Time Complexity = O(m + n)
```

✅ **Not `m * n`**
✅ Because we **don’t visit all cells**

---

## Visual Way to Remember 🧠

Think of a path like this:

```
→ → → ↓ ↓ ↓ → ↓
```

You are **walking once across columns** and **once across rows** — not zig-zagging everywhere.

---

## Why some people wrongly say O(m*n)?

Because:

* They think “nested matrix = m*n”
* But **this is NOT nested traversal**
* It’s a **single path traversal**

---

## One-Line Interview Answer 💬

> “Each step removes one row or one column, so total steps are at most m+n.”

Say this calmly — interviewers love this answer.

---

## Quick Comparison

| Approach         | Time        |
| ---------------- | ----------- |
| Brute force      | O(m*n)      |
| Staircase search | **O(m+n)**  |
| Binary search    | O(log(m*n)) |

---


