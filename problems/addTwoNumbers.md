# Add Two Numbers

## The Problem
https://leetcode.com/problems/add-two-numbers/

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Thoughts

### pass 1

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
### pass 2
I got much further into the solution for the problem. This has definetly forced me to get a better idea of what a nodelist is and how it functions. 

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
        ListNode *sum = l2;   
 
        while(l1!=NULL && l2!=NULL){
            std::cout<< "value of l1 " << l1->val << endl << endl;
            std::cout<<"before l1="<<l1->val << " l2="<< l2->val << " sum=" << sum->val << std::endl;
            if(l1->val == -1){
                std::cout<<"if -1 l1="<<l1->val << " l2="<< l2->val << " sum=" << sum->val << std::endl;
                l2->val +=1;
                l1 = l1->next;
                
                continue;
            }
            int temp = l1->val + l2->val;
            if(temp >=10){
                temp -=10;
                l1->val = -1;
                sum->val = temp;
                std::cout<<"if over l1="<<l1->val << " l2="<< l2->val << " sum=" << sum->val << std::endl;
                if(l2->next == NULL){
                    std::cout<<"lol" << std::endl;
                    if(l1->next== NULL){
                        l2->next = new ListNode(0);
                        std::cout<<"end of l1 nodes"<< std::endl;
                    } else{
                        l2->next = new ListNode(0);
                        std::cout<<"end of l2 nodes"<< std::endl;
                    }
                    std::cout<<"end of nodes"<< std::endl;
                    addTwoNumbers(l1,l2);
                    return sum;
                    
                }
                else if(l1->next == NULL){
                    l1->next = new ListNode(0);
                    l2->next = new ListNode(0);
                    std::cout<<"end of nodes"<< std::endl;
                    addTwoNumbers(l1,l2);

                    return sum;
                }
                else{
                l2 = l2->next;
                addTwoNumbers(l1,l2);
                return sum;
                }
            }
            else{
                sum->val = temp;
                std::cout<<"not over l1="<<l1->val << " l2="<< l2->val << " sum=" << sum->val << std::endl;
                if(l2->next == NULL && l1->next != NULL){
                    l2->next = new ListNode(0);
                }
                l1 = l1->next;
                l2 = l2->next;
                addTwoNumbers(l1,l2);

            }
            return sum;
        }

        return sum;
        
    }
};
```
