```
else goto step (5)
3. if(key[middle] = target)
   (Position = middle, flag = 1
   Goto step (5)
   else if(key[middle] > target) then
       high = middle - 1
   else
       low = middle + 1
4. Goto step(2)
5. if flag = 1
   report as target element found at location 'position'
   else
   report that element is not found in the list
6. stop
```

The effectiveness of the binary search algorithm lies in its continual halving of the list to be searched. For an ordered list of 50,000 keys, the worst case efficiency is a mere 16 accesses. One may note that the dramatic increase in efficiency is noticed as the list gets larger. We can check with a calculator as to how many times 50,000 must be halved to be reduced to 1. The same list that would have necessitated an average wait of two minutes using a sequential search will give a virtually instantaneous response when the binary search is used. In more precise algebraic terms, the halving method yields a worst case search efficiency of log2n.

A non-recursive code in C++ that demonstrates the implementation of Algorithm 9.3 is given in Program Code 9.3 and a recursive code for the same is given in Program Code 9.4.

```
PROGRAM CODE 9.3
int Binary_Search_non_recursive(int A[], int n, int key)
{
int low = 0, high = n-1,mid;
while (low <= high)
{ //iterate while first <= last
mid = (low + high)/2; //calculate
mid = (first + last)/2;
if(A[mid] == key)
return mid; //return position (mid)
else if(key<A[mid])
//not found; look in upper half of list
high = mid - 1;
else
low = mid + 1; //look in lower half
}
return -1; //return "not found"
}
```