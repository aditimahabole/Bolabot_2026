# LC2095 – Delete the Middle Node of a Linked List

## 🔹 Problem Summary
You are given the **head of a singly linked list**.

Your task is to:
- Delete the **middle node**
- Return the head of the modified list

### Definition of Middle
- For a list of size `n`
- Middle index = `n / 2` (0-based index)
- If `n` is even, **second middle** is deleted

---

## 🧠 Core Idea (Why This Works)

We need to:
1. Find the **middle node**
2. Remove it safely

But we want to do this in **one traversal**, not two.

👉 This is a **classic Slow & Fast Pointer problem**.

---

## 🚀 Approach: Slow & Fast Pointer Technique

### Step-by-step Logic

1. Use two pointers:
   - `slow` → moves **1 step**
   - `fast` → moves **2 steps**
2. When `fast` reaches the end:
   - `slow` will be at the **middle node**
3. Maintain a `prev` pointer:
   - Points to the node **just before `slow`**
4. Delete the middle node by:
   - `prev.next = slow.next`

---

## 🧪 Edge Cases (Very Important in Interviews)

| Case | Action |
|----|----|
| Empty list | Return `NULL` |
| Single node | Return `NULL` (list becomes empty) |
| Two nodes | Delete second node |

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)` (no extra memory)

---

## 💡 Interview Memory Trick

> ❝Fast moves twice as fast, slow finds the middle❞

And:
> ❝To delete any node, you must know the node before it❞ → hence `prev`

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
    ListNode* deleteMiddle(ListNode* head) {
        // Edge case: empty or single node
        if (head == NULL || head->next == NULL)
            return NULL;

        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* prev = NULL;

        // Move slow by 1 and fast by 2
        while (fast != NULL && fast->next != NULL) {
            prev = slow;
            slow = slow->next;
            fast = fast->next->next;
        }

        // Delete middle node
        prev->next = slow->next;
        delete slow;

        return head;
    }
};
