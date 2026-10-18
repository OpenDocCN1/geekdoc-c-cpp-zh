```
```cpp
template <class T>
void display(T x)        //overloaded template function display
{
    cout<<"Overloaded Template Display 1: "<<x<<"\n";
}
template <class T, class T1>
void display(T x, T1 y)        //overloaded template function
display
{
    cout<<"Overloaded Template Display 2: "<<x<<", "
    <<y<<"\n";
}
void display(int x)        //overloaded generic display function
{
    cout<<"Explicit display: "<<x<<"\n";
}
int main()
{
    display(100);
    display(12.34);
    display(100,12.34);
    display('C');

    return 0;
}
```
```

The output of Program 12.9 would be:

+   Explicit display: 100
+   
+   Overloaded Template Display 1: 12.34
+   
+   Overloaded Template Display 2: 100, 12.34
+   
+   Overloaded Template Display 1: C