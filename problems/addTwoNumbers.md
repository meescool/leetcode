# Add Two Numbers

## The Problem
https://leetcode.com/problems/add-two-numbers/

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Thoughts

Still need to finish

``` c++
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        // ListNode* sum = new(sise);
        ListNode *sum = new ListNode();   
        ListNode temporary = ListNode();
        int extra = 0;
        sum->val = 0;
        while(l1!=NULL){           

            int temp = l1->val + l2->val;
            if(temp >= 10){                
                temp -=10;
                extra = 1;
            }
            
            sum->val = temp;
            l1 = l1->next;
            l2 = l2->next;
            sum = sum->next;

            extra = 0;
                
            addTwoNumbers(l1,l2);

        }

        return sum;
        
    }
};
```
