# LC876 – Middle of the Linked List

## 🔹 Problem Summary
You are given the **head of a singly linked list**.

Your task is to:
- Return the **middle node** of the linked list
- If there are **two middle nodes** (even length list), return the **second middle**

---

## 🧠 Key Insight
To find the middle efficiently:
- Avoid counting nodes first
- Avoid extra space

👉 Use the **Slow & Fast Pointer technique**

---

## 🚀 Approach: Slow and Fast Pointers

### How it works
- `slow` moves **one step at a time**
- `fast` moves **two steps at a time**

When `fast` reaches the end of the list:
- `slow` will be pointing to the **middle node**

This automatically satisfies the requirement:
- For even-length lists, `slow` lands on the **second middle**

---

## 🧪 Example Walkthrough

### Example 1
List: `1 → 2 → 3 → 4 → 5`

Steps:
- slow = 1, fast = 1
- slow = 2, fast = 3
- slow = 3, fast = 5

✅ Middle = `3`

---

### Example 2 (Even length)
List: `1 → 2 → 3 → 4 → 5 → 6`

Steps:
- slow = 1, fast = 1
- slow = 2, fast = 3
- slow = 3, fast = 5
- slow = 4, fast = null

✅ Middle = `4` (second middle)

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

Only one traversal, no extra memory.

---

## 💡 Interview Memory Trick

> ❝Fast runs twice as fast, slow finds the middle❞

If the interviewer asks *why second middle?*  
👉 Because `slow` moves only when `fast` moves twice.

---

## 🧾 C++ Implementation

```cpp
/**
 * Definition for singly-linked list.
 */
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;

        // Move slow by 1 and fast by 2
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
        }

        return slow;
    }
};
