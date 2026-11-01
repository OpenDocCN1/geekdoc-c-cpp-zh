```
// C#
public class Singleton
{
    private static SomeData data = null;
    public static SomeData GetData()
    {
        if (data == null)
        {
            data = new SomeData();
        }
        return data;
    }
}
// use:
SomeData d = Singleton.GetData();
```

code snippet CSharp/Singleton.cs

```
// C++/CLI
public ref class Singleton
{
private:
    static SomeData* hData;
public:
    static SomeData* GetData()
    {
        if (hData == nullptr)
        {
            hData = gcnew SomeData();
        }
        return hData;
    }
};
// use:
SomeData* d = Singleton::GetData();
```

code snippet CPPCLI/Singleton.h

```
' Visual Basic
Public Class Singleton
    Private Shared data As SomeData
    Public Shared Function GetData() As SomeData
        If data Is Nothing Then
            data = new SomeData()
        End If
        Return data
    End Function
End Class
' Use:
Dim d as SomeData = Singleton.GetData()
```

code snippet VisualBasic/Singleton.fs

# ARRAYS

Arrays are discussed in Chapter 6, "Arrays and Tuples." The Array class is always behind the scenes of .NET arrays; declaring an array, the compiler creates a class that derives from the Array base class. When C# was designed, the designers of the C# language took the bracket syntax for arrays from C++ and extended it with array initializers:

```
// C#
int[] arr1 = new int[] { 1, 2, 3};
int[] arr2 = {1, 2, 3};
```