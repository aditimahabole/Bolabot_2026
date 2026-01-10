# 237. Delete Node in a Linked List

## 🔹 Problem Summary
You are given **only the node to be deleted**, not the head of the linked list.

Constraints:
- Singly linked list
- All values are unique
- The given node is **not the last node**

Goal:
Delete the given node such that:
- The value disappears from the list
- List size decreases by 1
- Order of remaining nodes stays same

---

## 🧠 Key Insight (Most Important)
👉 Since we **don’t have access to the previous node or head**,  
👉 We **cannot** delete the node directly.

### 🔑 Trick:
**Copy the next node’s value into the current node, then skip the next node.**

---

## ✅ Correct & Optimal Approach

1. Copy `node.next.val` into `node.val`
2. Make `node.next` point to `node.next.next`
3. Done ✅

⏱ Time Complexity: **O(1)**  
📦 Space Complexity: **O(1)**

---

## ❌ Why Shifting Values Is Unnecessary
Your solution shifts values until the end and deletes the last node.

Problems with that:
- Takes **O(n)** time instead of O(1)
- Over-complicates a trick-based question
- Interviewers expect the **copy-and-skip** method

---

## 💡 Interview Memory Trick
> ❝You can’t remove yourself — become the next guy and kill him❞ 😄

(Replace your value with next node’s value and remove next node)

---

## 🧪 Example
List: `4 → 5 → 1 → 9`  
Delete node = `5`

Steps:
- Copy `1` into `5`
- Remove original `1`

Result: `4 → 1 → 9`

---

## 🧾 C++ Solution

```cpp
/**
 * Definition for singly-linked list.
 */
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
