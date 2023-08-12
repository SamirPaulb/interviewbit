# Sum of minimum and maximum elements of all subarrays of size k

https://www.interviewbit.com/problems/sum-of-minimum-and-maximum-elements-of-all-subarrays-of-size-k/

Given an array A of both positive and negative integers.

Your task is to compute sum of minimum and maximum elements of all sub-array of size B.

### Note

Since the answer can be very large, you are required to return the sum module 1000000007.

### Input Format

```
The first argument denotes the array A.
The second argument denotes the value B
```

### Output Format

Return an integer that denotes the required value.


### Constraints

```
1 <= size of array A <= 100000
-1000000000 <= A[i] <= 1000000000
1 <= B <= size of array
```

###  Example
```
Input 1:
    A[] = {2, 5, -1, 7, -3, -1, -2}
    B = 4
    
Output 1:
    18
Explanation : 
    Subarrays of size 4 are : 
        {2, 5, -1, 7},   min + max = -1 + 7 = 6
        {5, -1, 7, -3},  min + max = -3 + 7 = 4      
        {-1, 7, -3, -1}, min + max = -3 + 7 = 4
        {7, -3, -1, -2}, min + max = -3 + 7 = 4   
        Sum of all min & max = 6 + 4 + 4 + 4 
                             = 18 
```
## Solution

### Editorial
```cpp
// no official solution provided
```

### Mine
```cpp
#define N 1000000007
int Solution::solve(vector<int> &a, int k) {
    long long x = 0;    
    deque<int> s, g;
    for (int i = 0; i < a.size(); i++) {
        while (!s.empty() && a[i] >= a[s.front()]) s.pop_front();
        while (!g.empty() && a[i] <= a[g.front()]) g.pop_front();
        s.push_front(i);
        g.push_front(i);
        if (s.back() <= i - k) s.pop_back();
        if (g.back() <= i - k) g.pop_back();
        if (i >= k - 1) x += a[s.back()] + a[g.back()];
    }
    return (x % N + N) % N;
}
```
### G4G
```cpp
int Solution::solve(vector<int> &arr, int k) {
    long long sum = 0;
    int n = arr.size();
    deque<int> S(k), G(k);
    int i = 0;

    for (i = 0; i < k; i++) {
        while ((!S.empty()) && arr[S.back()] >= arr[i])
            S.pop_back();
        while ((!G.empty()) && arr[G.back()] <= arr[i])
            G.pop_back();
        G.push_back(i);
        S.push_back(i);
    }

    for (; i < n; i++) {
        sum += arr[S.front()] + arr[G.front()];
        while (!S.empty() && S.front() <= i - k)
            S.pop_front();
        while (!G.empty() && G.front() <= i - k)
            G.pop_front();
        while ((!S.empty()) && arr[S.back()] >= arr[i])
            S.pop_back();
        while ((!G.empty()) && arr[G.back()] <= arr[i])
            G.pop_back();
        G.push_back(i);
        S.push_back(i);
    }
    sum += arr[S.front()] + arr[G.front()];
    return (sum % 1000000007 + 1000000007) % 1000000007;
}

```
### Python
```python
from collections import deque 

class Solution:
    def solve(self, arr, k):
        Sum = 0
        n = len(arr)
        S = deque()
        G = deque()
    
        for i in range(k):
            while ( len(S) > 0 and arr[S[-1]] >= arr[i]): 
                S.pop() # Remove from rear 
            while ( len(G) > 0 and arr[G[-1]] <= arr[i]): 
                G.pop() # Remove from rear 
    
            G.append(i)
            S.append(i)
    
        for i in range(k, n):
            Sum += arr[S[0]] + arr[G[0]] 
            while ( len(S) > 0 and S[0] <= i - k): 
                S.popleft() 
            while ( len(G) > 0 and G[0] <= i - k): 
                G.popleft() 
            while ( len(S) > 0 and arr[S[-1]] >= arr[i]): 
                S.pop() # Remove from rear 
            while ( len(G) > 0 and arr[G[-1]] <= arr[i]): 
                G.pop() # Remove from rear 
            G.append(i) 
            S.append(i)
            
        Sum += arr[S[0]] + arr[G[0]]
        return Sum % 1000000007
```
