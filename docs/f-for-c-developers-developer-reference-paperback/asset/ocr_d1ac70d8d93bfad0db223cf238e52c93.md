```
//use reflection to invoke SetStudentInfo method
let result = studentType.GetMethod("SetStudentInfo").Invoke(student, [| "Brent"; 18 |])

```

```
printfn "new student info: name = %s, id = %d" student.Name student.ID
```

Execution result

Created a student object
new student info: name = Brent, id = 18

# Using Reflection on F# Types

Reflection was introduced before F# came into production, so F# needed a way to provide reflection on its specific types, such as a tuple. You can find all of these F# specific reflection functions in the Microsoft.FSharp.Reflection namespace.

# Using Tuples

Listing 6-114 shows how to use reflection to get the element types in a tuple, get element values, and make a tuple from an object array.

LISTING 6-114 F# reflection on a tuple

```
source code

op Microsoft.FSharp.Reflection

let tuple = ("John", 18, "Canada")

// get element types in a tuple
FSharp.Type.GetTupleElements(tuple.GetType())

// retrieve given tuple value
FSharpValue.GetTupleField(tuple, 2)

// retrieve all fields in a tuple
FSharpValue.GetTupleFields(tuple)

// make a tuple from an array array
FSharpValue.MakeTuple([| "Lisa"; 20; "USA" |], tuple.GetType())

// check if a type is a tuple
FSharp.Type.IsTuple(tuple.GetType())

// make a tuple
let t = FSharpType.MakeType([| typeof<int>; typeof<string> |])
FSharpValue.MakeTuple([| "One"; |], t)
```