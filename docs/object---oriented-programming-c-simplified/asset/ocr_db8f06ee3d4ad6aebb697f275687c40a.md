```
```cpp
void main()
{
    demo<int>d1;
    cout << “Sum =” << d1.sum() << endl;
    demo<float>d2;
    cout << “Sum =” << d2.sum() << endl;
    demo<long>d3;
    cout << “Sum =” << d3.sum() << endl;
}
```
```

# **OUTPUT:**

Enter 5 int numbers  
2 45 67 34 23  
Sum = 169  
Enter 5 float numbers  
1.2 3.4 3.3 4.5 5.6  
Sum = 18  
Enter 5 long numbers  
12345  
234567  
76543  
34567  
127865  
Sum = 485815

**EXPLANATION:** The class template is created for declaring and defining arrays of different types and finding sum of its elements. When **demo<float>d2;** executes a new version of demo class template is instantiated and all prompt user for 5 elements. Numbers are stored in the array and sum is displayed by a call to sum function using object d2. The class will look like as:

```
```cpp
class demo
{
    float arr[S];
public:
    demo()
    {
        int i;
        cout << “Enter ” << S << “ ” << typeid(float).name()
             << “ numbers\n”;
        for(i = 0; i < S; i++)
```
```