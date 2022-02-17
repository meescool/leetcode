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
### pass 3
I finally was able to solve the problem!
It really helped to write down all my ideas before starting, and having a clear structure set in my head.
It also helped that my mind was able to focus a lot easier. 
The issues I had were mainly due to figuring out how to deal with the extra nodes when the lists were of different sizes.
Overall, I'm pretty happy to have been able to find a solution for the problem, though I later found out there were better solutions to this problem :')
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
                /**
        create a new sum node
        loop through the nodes from l1 and l2
        once both are null exit
            
            sum nodes from l1 and l2 and add to sum
            if the sum is over 9
                subtract ten from the sum
                then create a new node to the sum and set it to one
                
            else the sum is <= 9 
                add a new node to sum
                set l1 and l2 to equal the next node
            call addTwoNumbers with l1 and l2 as params
            return sum
        **/
        ListNode *sum = l2;

        while(l1 != NULL && l2 != NULL){
            // incase we need to carry 1 one over 
            if(l1->val == -1){
                l2->val += 1;
                if(l1->next == NULL){
                    l1->next = new ListNode(0);
                    l1 = l1->next;
                } else{
                    l1 = l1->next;
                }
                continue;
            }
            // otherwise continue to add
            sum->val = l1->val + l2->val;
            // if answer is over 10 then subtract 10 to result
            if (sum->val >= 10){
                sum->val -= 10;
                // let l1 equal -1 to let the program know there is one leftover
                l1->val= -1;
                // incase the both lists ends or just l2 ends, add a new node to l2
                if((l1->next == NULL && l2->next==NULL) || (l1->next != NULL && l2->next==NULL) )
                {
                    l2->next = new ListNode(0);
                } // incase l2 ends early, add anew 
                
                l2 = l2->next;
                
            } 
            else // if the answer is less then 10
            {
                // check if any of the linked lists end early to add a new node
                if(l1->next != NULL && l2->next==NULL){
                    l2->next = new ListNode(0);
                } else if(l1->next == NULL && l2->next!=NULL ){
                    l1->next = new ListNode(0);
                }
                // go to the next node
                l1 = l1->next;
                l2 = l2->next;
                
            }
            
            // call itself to go to the next node
            addTwoNumbers(l1,l2);
            
            // return sum
            return sum;
        } 
        return l1;
    }
};
```
