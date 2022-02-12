# First Bad Version

## The Problem

https://leetcode.com/problems/first-bad-version/

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

```
Example 1:

Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.
```

## Thoughts

In order to find the first bad version, I knew that using a binary search would help. I realized that there are different ways to implement this type of algorithm, and was able to do it in a more simple manner compared to how I have done it before. 
    
```c++
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int middle = 1;
        int high = n;
        int low = 1;
        int check = false;
        
        while(true){
            middle = low + ((high - low)/2) ;
            
            check = isBadVersion(middle); 
            if(check == true && isBadVersion(middle-1) == false){
                return middle;
            }

            if(check == false){
                low = middle + 1;
                printf("low %d \n", low);
            }
            if (check == true){
                high = middle - 1;
                printf("high %d \n", high);
            } 
        }
    }
};
```
