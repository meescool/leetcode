# Guess Number Higher or Lower

## The Problem

https://leetcode.com/problems/guess-number-higher-or-lower/

We are playing the Guess Game. The game is as follows:
I pick a number from 1 to n. You have to guess which number I picked.
Every time you guess wrong, I will tell you whether the number I picked is higher or lower than your guess.
You call a pre-defined API int guess(int num), which returns three possible results:

- 1: Your guess is higher than the number I picked (i.e. num > pick).
- 1: Your guess is lower than the number I picked (i.e. num < pick).
- 0: your guess is equal to the number I picked (i.e. num == pick).

Return the number that I picked.

 
```
Example 1:

Input: n = 10, pick = 6
Output: 6

```

## Thoughts

Used a binary search algorithm approach to find the number. It has a been a while since I have seen the code for this type of algorithm so I did my best to visualize what I remembered of this algorithm and how to implement it. It was interesting reading about the ternary search solution.
    
```c++
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is lower than the guess number
 *			      1 if num is higher than the guess number
 *               otherwise return 0
 * int guess(int num);
 */

class Solution {
public:
    int guessNumber(int n) {
        int middle = n/2; // starting at the midpoint
        int range = n/2; // the range
        int finalGuess = 0;
        if(n == 1 || guess(n) == 0){
            finalGuess = n;
        }
        else{
        
            // implementing a binary search ^.^, sorta
            while(true){            
                if(guess(middle) == 0){
                    finalGuess = middle;
                    break;
                }
                if(range == 1){
                    range +=1;
                }
                else{
                    // set the new range;
                    range = range / 2;
                }

                if(guess(middle) == -1){
                    // if too high then subtract the range from the middle for new middle
                    middle = middle - range;

                }
                if(guess(middle) == 1){
                    // if too high then subtract the range from the middle for new middle
                    middle = middle + range;
                }

            }
        }
                
        
        return finalGuess;
                      
        }

};
```
