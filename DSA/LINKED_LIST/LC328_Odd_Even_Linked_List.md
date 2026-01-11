# LC328 – Odd Even Linked List

## 🔹 Problem Statement
Given the head of a singly linked list, group all nodes at **odd indices** together
followed by the nodes at **even indices**.

- Indexing is **1-based**
- Relative order within odd and even groups must remain the same
- Must be done **in-place**

---

## 🧠 Approach

This problem is **NOT about node values** (odd/even values).  
It is purely about **node positions**.

### Key Idea
While traversing the list:
- Maintain two separate chains:
  - One for **odd-positioned nodes**
  - One for **even-positioned nodes**
- Finally, connect the odd list to the even list

---

### Step-by-Step Logic

1. If the list has `0` or `1` node, return it as-is
2. Initialize pointers:
   - `odd = head`
   - `even = head.next`
   - `evenHead = head.next` (important to reconnect later)
3. Traverse while `even` and `even.next` are not null:
   - `odd.next = even.next` → link next odd node
   - `even.next = even.next.next` → link next even node
   - Move `odd` and `even` forward
4. Attach even list after odd list:
   - `odd.next = evenHead`
5. Return `head`

---

## 🧾 C++ Code

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
    ListNode* oddEvenList(ListNode* head) {
        // Base case
        if (head == NULL || head->next == NULL)
            return head;

        ListNode* odd = head;
        ListNode* even = head->next;
        ListNode* evenHead = even;

        while (even != NULL && even->next != NULL) {
            odd->next = even->next;
            odd = odd->next;

            even->next = odd->next;
            even = even->next;
        }

        odd->next = evenHead;
        return head;
    }
};
````

---

## ☕ Java Code

```java
/**
 * Definition for singly-linked list.
 */
class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) {
        this.val = val;
    }
    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}

class Solution {
    public ListNode oddEvenList(ListNode head) {
        // Base case
        if (head == null || head.next == null)
            return head;

        ListNode odd = head;
        ListNode even = head.next;
        ListNode evenHead = even;

        while (even != null && even.next != null) {
            odd.next = even.next;
            odd = odd.next;

            even.next = odd.next;
            even = even.next;
        }

        odd.next = evenHead;
        return head;
    }
}
```

---

## ⏱ Time & Space Complexity

* **Time Complexity:** `O(n)`

  * Each node is visited exactly once
* **Space Complexity:** `O(1)`

  * Rearrangement is done in-place

---

## ⚠️ Base Cases & Critical Test Cases

### Empty List

```
Input:  []
Output: []
```

### Single Node

```
Input:  [1]
Output: [1]
```

### Two Nodes

```
Input:  [1,2]
Output: [1,2]
```

### Odd Number of Nodes

```
Input:  [1,2,3,4,5]
Output: [1,3,5,2,4]
```

### Even Number of Nodes

```
Input:  [1,2,3,4,5,6]
Output: [1,3,5,2,4,6]
```

---

## 💡 Interview Memory Trick

> “Make two lists (odd & even) and attach even after odd.”

Always remember:

* **Save `evenHead`**, otherwise the even list is lost

---

## 🧠 One-Line Summary

Split the list into odd and even position nodes in one pass and merge them.

