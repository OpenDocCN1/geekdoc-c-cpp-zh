```
Public NotInheritable Class Dog
Inherits Pet
End Class
```

```
Public NotInheritable Class Macaw
Inherits Pet
End Class
```

> Code file [Pet.vb] available for download at Wrox.com.

You, have abstract Pets with two concrete manifestations, Dog and Macaw. These types are intended to be used in a pet shop application, and so Pet has an operation named ShackUpWith sequences of pets and returns their own.

Modify the Module.vb file of the application as shown in Listing 22-7.

# LISTING 22-7: Module1.vb of CovarianceSample

![](bbox=[0.101, 0.375, 0.151, 0.403])

```
Option Strict On
Module Module

Sub Main()
    Dim Dogs As New List(Of Dog) From {
        New Dog(.NickName = "Spike", .Age = 3),
        New Dog(.NickName = "Murray", .Age = 12),
        New Dog(.NickName = "Peach", .Age = 2)
    }

    Dim Macaws As New List(Of Macaw) From {
        New Macaw(.NickName = "Georgey", .Age = 32),
        New Macaw(.NickName = "Bella", .Age = 4),
        New Macaw(.NickName = "Grey", .Age = 11)
    }

    Dim Youngsters =
        From pet In Pet.ShackUpWith(Dogs, Macaws)
        Where pet.Age < 5
        Select pet

    For pet In Youngsters
        Console.WriteLine(pet.NickName)
    Next
End Sub
End Module
```



The ShackUpWith method used in the query expression expresses IEnumerable(Of Pet) arguments. But in the previous code, IEnumerable(Of Dog) and IEnumerable(Of Macaw) instances are passed.