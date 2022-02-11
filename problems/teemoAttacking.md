# Teemo Attacking

## The Problem
https://leetcode.com/problems/teemo-attacking/

Our hero Teemo is attacking an enemy Ashe with poison attacks! When Teemo attacks Ashe, Ashe gets poisoned for a exactly duration seconds. More formally, an attack at second t will mean Ashe is poisoned during the inclusive time interval [t, t + duration - 1]. If Teemo attacks again before the poison effect ends, the timer for it is reset, and the poison effect will end duration seconds after the new attack.

You are given a non-decreasing integer array timeSeries, where timeSeries[i] denotes that Teemo attacks Ashe at second timeSeries[i], and an integer duration.

Return the total number of seconds that Ashe is poisoned.

```
Example 1:

Input: timeSeries = [1,4], duration = 2
Output: 4
Explanation: Teemo's attacks on Ashe go as follows:
- At second 1, Teemo attacks, and Ashe is poisoned for seconds 1 and 2.
- At second 4, Teemo attacks, and Ashe is poisoned for seconds 4 and 5.
Ashe is poisoned for seconds 1, 2, 4, and 5, which is 4 seconds in total.
```

## Thoughts
Used a for loop to go through each of the times that the Teemo attacked Ashe, and realized that it would be optimal to find a way to compare each of the elements with how much time was in between and then take into consideration how much the poisoning lasted. I they got attacked while they were still poisoned, then I just needed to add the amount of time that passed between attacks, which would indicate that the duration was reset and would move on to the next attack.
```c++
class Solution {
public:
    int findPoisonedDuration(vector<int>& timeSeries, int duration) {
        int poisonTime = duration; // initializing poisonTime to duration since the first attack is bound to happen
        
        for(int i = 0; i < timeSeries.size(); i++){
            if(i > 0){
                if( timeSeries[i] - timeSeries[i-1] < duration ){
                    poisonTime += timeSeries[i] - timeSeries[i-1]; // add only the amount of time 
                                                                   // that passed before getting attacked again
                }
                else{
                     poisonTime += duration; // add the time that poisoned
                }
            }
            
            
        }
        return poisonTime;
    }
};
```
