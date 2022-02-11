# Teemo Attacking

## The Problem
Our hero Teemo is attacking an enemy Ashe with poison attacks! When Teemo attacks Ashe, Ashe gets poisoned for a exactly duration seconds. More formally, an attack at second t will mean Ashe is poisoned during the inclusive time interval [t, t + duration - 1]. If Teemo attacks again before the poison effect ends, the timer for it is reset, and the poison effect will end duration seconds after the new attack.

You are given a non-decreasing integer array timeSeries, where timeSeries[i] denotes that Teemo attacks Ashe at second timeSeries[i], and an integer duration.

Return the total number of seconds that Ashe is poisoned.

## Thoughts
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
