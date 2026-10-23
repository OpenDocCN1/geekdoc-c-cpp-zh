In the following example, we have depicted how the class template can be used to define a type that will be applicable and accessible through the class:

```
Program: Use of class template
const int size=4;
template<class t>
class one
{
t a[size];  // declaring the t type
public:
one(t[]);
void sum();
};
template<class t>
one<t>::one(t aa[])
{
for(int i=0;i<size;i++)
a[i]=aa[i];
}
template<class t>
void one<t>::sum()      // defining the function outside the class
{
t s=0;
for(int i=0;i<size;i++)
s=s+a[i];        // adding the number one by one
cout<<" sum of all numbers: "<<s<<endl;
}
int main()
{
clrscr();
int arr[]={2,3,4,5};
float farr[]={2.5,3.2,4.6,5.9};
one<int> a(arr); // creating the template as integer type
one<float> b(farr);    // creating the template as float type
a.sum();
cout<<" Sum of float array"<<endl;
```