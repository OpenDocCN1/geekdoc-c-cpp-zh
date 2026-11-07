![](bbox=[0.182, 0.107, 0.912, 0.709])

**FIGURE 18-38**  Execution of the statement `reversePrint(first);`

# printListReverse

Now that we have written the function reversePrint, we can write the definition of the function printListReverse. Its definition is:

```
```cpp
template <class Type>
void LinkedListType<Type>::printListReverse() const
{
    reversePrint(first);
    cout << endl;
}
```
```