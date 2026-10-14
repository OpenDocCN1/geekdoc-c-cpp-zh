# Important

Be sure to add the code to the correct implementation of the Current property. Leave the nongeneric version, System.Collections.IEnumerator.Current, with its default implementation that throws a NotImplementedException exception.

The Current property examines the enumData variable to ensure that MoveNext has been called. (This variable will be null prior to the first call to MoveNext.) If this is not the case, the property throws an InvalidOperationException—this is the conventional mechanism used by .NET Framework applications to indicate that an operation cannot be performed in the current state. If MoveNext has been called beforehand, it will have updated the currentItem variable, so all the Current property needs to do is return the value in this variable.

12. Locate the IDisposable.Dispose method. Comment out the throw new NotImplemented-Exception(); statement as shown in bold in the code that follows. The enumerator does not use any resources that require explicit disposal, so this method does not need to do anything. It must still be present, however. For more information about the Dispose method, refer to Chapter 14.

Click here to view code image

```
void IDisposable.Dispose()
{
    // throw new NotImplementedException();
}
```

13. Build the solution, and correct errors if any are reported.