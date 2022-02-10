# Fizz Buzz

## The Problem

https://leetcode.com/problems/fizz-buzz/

Given an integer n, return a string array answer (1-indexed) where:

answer[i] == "FizzBuzz" if i is divisible by 3 and 5.
answer[i] == "Fizz" if i is divisible by 3.
answer[i] == "Buzz" if i is divisible by 5.
answer[i] == i (as a string) if none of the above conditions are true.

## Example

'''
<b>Input:<b> n = 3
<b>Output:<b> ["1","2","Fizz"]
'''

## Thoughts

I know that using the modulus operand returns a 0 if a number is multiple of another. The next step was figuring out the correct way to implement the solution.
I quickly found out that arrays needs to be given a size, so I had to find a way to implement a dynamic array of strings. For the solutions I made use of a vector of strings.

## Solution
'''
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        std::vector<std::string> answer(n);
        for(int i = 1; i <= n; i++){
            if(i%3 == 0 && i%5 == 0){
                answer[i-1] = "FizzBuzz";
            } else if(i%3 == 0 && i%5 != 0){
                answer[i-1] = "Fizz";
            } else if (i%3 != 0 && i%5 == 0){
                answer[i-1] = "Buzz";
            } else {
                answer[i-1] = to_string(i) ;
            }
            
        }
        return answer;
        
    }
};
'''