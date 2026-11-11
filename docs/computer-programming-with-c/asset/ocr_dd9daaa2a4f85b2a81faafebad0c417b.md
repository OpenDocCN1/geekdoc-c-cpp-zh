```
```cpp
}
int isempty()
{
        return (size==0);
};
void main()
{
Queue<int> q;
q.add(10);
cout<<"Added 10"<<endl;
q.add(20);
cout<<"Added 20"<<endl;
q.add(30);
cout<<"Added 30"<<endl;
cout<<"**********Order of removing
elements**************"<<endl;
int temp;
while (!q.isempty())
{
        temp =q.remove();
        cout<<temp<<endl;
}
}
```
```

# Output

```
```text
Added 10
Added 20
Added 30
**********Order of removing elements**************
10
20
30
```
```

# Error Finding Exercise

The following are some programs that may or may not contain errors. Correct the errors if they exist in the code and determine the output after applying the corrections.

# Program 1

```
```cpp
template <class G>
int a=0,b=0;
G add(G a,G b)
{
```
```