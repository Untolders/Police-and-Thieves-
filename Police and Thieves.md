Given an array arr[], where each element contains either a 'P' for policeman or a 'T' for thief. Find the maximum number of thieves that can be caught by the police. 
Keep in mind the following conditions :

Each policeman can catch only one thief.
A policeman cannot catch a thief who is more than k units away from him.
Examples:
```
Input: arr[] = ['P', 'T', 'T', 'P', 'T'], k = 1
Output: 2
Explanation: Maximum 2 thieves can be caught. First policeman catches first thief and second police man can catch either second or third thief.
```
```
Input: arr[] = ['T', 'T', 'P', 'P', 'T', 'P'], k = 2
Output: 3
Explanation: Maximum 3 thieves can be caught.
```
Constraints:
1 ≤ arr.size() ≤ 105
1 ≤ k ≤ 1000
arr[i] = 'P' or 'T'

```cpp
class Solution {
  public:
    int catchThieves(vector<char> &arr, int k) {
     int n = arr.size();
        int m = k+1;
        int count = 0;
        deque<int>police;
        deque<int>thief;
            
        for(int i=0;i<n;i++){
            if(arr[i]=='P'){
                if(thief.empty()){
                    police.push_back(i);
                }
                else{
                    while(!thief.empty() && i-thief.front()>k){
                        thief.pop_front();
                    }
                    if(!thief.empty()){
                        thief.pop_front();
                        count++;
                    }
                }
            }
            else{
                if(police.empty()){
                    thief.push_back(i);
                }
                else{
                    while(!police.empty() && i-police.front()>k){
                        police.pop_front();
                    }
                    if(!police.empty()){
                        police.pop_front();
                        count++;
                    }
                }
            }
        }
        return count;
    }
};
```
