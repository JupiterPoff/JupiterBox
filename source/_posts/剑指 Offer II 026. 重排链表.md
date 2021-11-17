---
剑指 Offer II 026. 重排链表
date: 2020-06-24 10:39:35 +0800
categories: Leetcode
mathjax: false
---

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    void reorderList(ListNode* head) {
       ListNode pseudoHead;
       pseudoHead.next = head;
       ListNode *slow=&pseudoHead,*fast =slow;
       while(fast&&fast->next)
       {
           slow=slow->next;
           fast=fast->next->next;
       }
       ListNode* half=slow->next;
       slow->next=nullptr;
       ListNode* re_half=myReverse(half);
       while(re_half)
       {
           ListNode* temp=head->next;
           head->next=re_half;
           ListNode* t = re_half->next;
           re_half->next = temp;
           re_half=t;
           head=temp;
       }
    }

private:
    ListNode* myReverse(ListNode* head)
    {
        if(!head) return nullptr;
        ListNode *pre=nullptr,*next=nullptr;
        while(head)
        {
            next=head->next;
            head->next=pre;
            pre=head;
            head=next;
        }
        return pre;
    }
};

```
