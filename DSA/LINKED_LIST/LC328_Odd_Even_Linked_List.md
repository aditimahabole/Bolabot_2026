# LC328 – Odd Even Linked List

## 🔹 Problem Statement
Given the head of a singly linked list, group all nodes at **odd indices** first,
followed by nodes at **even indices**.

- Indexing is **1-based**
- Relative order within odd and even nodes must be preserved
- Must be done **in-place**

---

## 🧠 Approach (How to Think)

This problem is **not about node values**, only about **positions**.

### Key Idea
Create **two chains** while traversing the list:
- One for **odd-positioned nodes**
- One for **even-positioned nodes**

Finally, attach the even list after the odd list.

---

### Step-by-Step Algorithm

1. If the list has **0 or 1 node**, return it directly
2. Initialize:
   - `odd = head`
   - `even = head.next`
   - `evenHead = head.next` (important to reconnect later)
3. Traverse while `even` and `even.next` are not null:
   - Link next odd node: `odd.next = even.next`
   - Link next even node: `even.next = even.next.next`
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
