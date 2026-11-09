Now let me explain exactly what is going on here. Upon entering the method, **currentVal** is initialized to the value in **target** at the moment the method starts executing. Then, inside the loop, **startVal** is initialized to this same value. Using **startVal**, you can perform any operation you desire. This operation can be extremely complex, consisting of thousands of lines of code. But, ultimately, you must end up with a result that is placed into **desiredVal**. In my example, I simply determine whether **startVal** or **value** contains the larger value.

Now, while this operation is running, another thread could change the value in **target**. It is unlikely that this will happen, but it is possible. If this does happen, then the value in **derivedVal** is based off an old value in **startVal**, not the current value in **target**, and therefore, we should not change the value in **target**. To ensure that the value in **target** is changed to **desiredVal** if no thread has changed **target** behind our thread's back, we use **Interlocked.CompareExchange**. This method checks if the value in **target** matches the value in **startVal** (which identifies the value that we thought was in **target** before starting to perform the operation). If the value in **target** didn't change, then **CompareExchange** changes it to the new value in **desiredVal**. If the value in **target** did change, then **CompareExchange** does not alter the value in **target** at all.

**CompareExchange** returns the value that is in **target** at the time when **CompareExchange** is called, which I then place in **currentVal**. Then, a check is made comparing **startVal** with the new value in **currentVal**. If these values are the same, then a thread did not change **target** behind our thread's back, **target** now contains the value in **desiredVal**, the **while** loop does not loop around, and the method returns. If **startVal** is not equal to **currentVal**, then a thread did change the value in **target** behind our thread's back, **target** did not get changed to our value in **desiredVal**, and the **while** loop will loop around and try the operation again, this time using the new value in **currentVal** that reflects the other thread's change.

Personally, I have used this pattern in a lot of my own code and, in fact, I made a generic method, **Morph**, which encapsulates this pattern⁷:

```
```csharp
delegate Int32 Morpher<TResult, TArgument>(Int32 startValue, TArgument argument,
    out TResult morphResult);

static TResult Morph<TResult, TArgument>(ref Int32 target, TArgument argument,
    Morpher<TResult, TArgument> morpher) {

    TResult morphResult;
    Int32 currentVal = target, startVal, desiredVal;
    do {
        startVal = currentVal;
        desiredVal = morpher(startVal, argument, out morphResult);
        currentVal = Interlocked.CompareExchange(ref target, desiredVal, startVal);
    } while (startVal != currentVal);
    return morphResult;
}
```
```

⁷ Obviously, the **Morph** method incurs a performance penalty due to invoking the **morpher** callback method. For best performance, execute the operation inline, as in the **Maximum** example.