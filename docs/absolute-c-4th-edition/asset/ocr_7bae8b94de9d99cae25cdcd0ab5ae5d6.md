# Display 16.9 Implementation for the Template Class PFArrayBak (part 2 of 3)

```
{
    b = new T[getCapacity()];
}

template<class T>
PFArrayBak<T>::PFArrayBak(int capacityValue)
    : PFArray<T>(capacityValue), usedB(0)
{
    b = new T[getCapacity()];
}

template<class T>
PFArrayBak<T>::PFArrayBak(const PFArrayBak<T>& oldObject)
    : PFArray<T>(oldObject), usedB(0)
{
    b = new T[getCapacity()];
    usedB = oldObject.getNumberUsed();
    for (int i = 0; i < usedB; i++)
        b[i] = oldObject.b[i];
}

template<class T>
void PFArrayBak<T>::backup()
{
    usedB = getNumberUsed();
    for (int i = 0; i < usedB; i++)
        b[i] = operator[](i);
}

template<class T>
void PFArrayBak<T>::restore()
{
    emptyArray();

    for (int i = 0; i < usedB; i++)
        addElement(b[i]);
}

template<class T>
PFArrayBak<T>& PFArrayBak<T>::operator =(const PFArrayBak<T>& rightSide)
{
    PFArray<T>::operator =(rightSide);

    if (getCapacity() != rightSide.getCapacity())
    {
        delete [] b;
        b = new T[rightSide.getCapacity()];
    }
}
```