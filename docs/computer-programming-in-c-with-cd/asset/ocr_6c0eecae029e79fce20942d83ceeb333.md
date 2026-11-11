```
```cpp
while((!found)&&(i<=N)) // assuming data array in ascending order
{
if(A[i]==data)
found=1;
else
i++;
}
if(found) cout<<"\\n found in location "<< i;
else
cout<<"\\n Not found";
}
void Dmanip :: Insert(int data)
{
int i=1, loc=1;
while ((data>A[i]) && (i<=N))// assuming data array in ascending order
i++;
if (data<= A[i])
{
loc=i;
for(i=N;i>=loc;i--)
A[i+1]=A[i];
}
A[loc]=data;
N=N+1;
}
void Dmanip :: Delete(int data)
{
int i=1, loc=1;
while ((data!=A[i]) && (i<=N))// assuming data array in random order
{
i++;
}
if (data== A[i])
{
loc=i;
for(i=loc;i<=N-1;i++)
A[i]=A[i+1];
N=N-1;
}
}
// Merging A of object 1 and A of object 2 resulting in A of object about
// which
// the merge function get referenced
```
```