# Program 16.9

```
/*To search an element in the given list using Linear search*/
#include<iostream.h>
#include<conio.h>
void main()
{
 int a[50],search,n,i;
 clrscr();
 cout<<"Enter Size Of Array:";
 cin>>n;
 cout<<"Enter "<<n<<" Elements:";
 for(i=0;i<n;i++)
 cin>>a[i];
 cout<<"Enter Search Element:";
 cin>>search;
 for(i=0;i<n;i++)
 {
 if(a[i]==search)
 {
 cout<<"Search Element"<<search<<"Is Found At"<<i+1<<"Location";
 getch();
 return;
 }
 }
 cout<<"Search Element"<<search<<"Is Not Found";
 getch();
}
```

# Output

Enter Size Of Array:6
Enter 6 Elements:4
8
9
1
2
3
Enter Search Element:2
Search Element 2 Is Found At 5 Location

# 16.2.2 BINARY SEARCH

Linear search so far discussed is simple and it is efficient if the list is small. Suppose to find a word in a dictionary performing linear search takes more time, whereas binary search instead of searching the dictionary from first to last, it opens the middle of the dictionary and searches that half of the dictionary which contains the word. Then again opening that half in the middle to find which quarter of it contains the word. Continuing like this, one can find the location of the word in the dictionary quickly since the number of possible locations to find it in the dictionary is reduced. This policy of searching is known as binary search and is better than linear search.