in a string – an equivalent of the nongeneric function we gave at the beginning of this section – and a sample call.

```
```
function Char_Count is new Generic_Count
    (Component_Type => Character,
     Index_Type      => Positive,
     Array_Type      => String);
```
```

```
```
The_Count := Char_Count (Source => "How now brown cow",
                         Pattern => 'w');
```
```

Writing a separate specification for nongeneric subprograms is optional. Generic subprograms must be written with separate specifications and bodies. The executable code of Generic_Count is identical to the original function we wrote for counting character occurrences in a string.

```
```
function Generic_Count (Source  : in  Array_Type;
                        Pattern : in  Component_Type) return Natural is
    Result : Natural := 0;
begin
    for Index in Source'Range loop
        if Source (Index) = Pattern then
            Result := Result + 1;
        end if;
    end loop;
    return Result;
end Generic_Count;
```
```

When writing the body, we have no idea of what actual types will be supplied for Array_Type and Component_Type. So, what operations can we apply to the parameters Source and Pattern? All we know about Source is that it is an unconstrained array indexed by some discrete type. We made use of the array attribute 'Range and array indexing in this body. We have no idea of the type of the parameter Pattern. However, we do know that it supports assignment and equality testing. It is only the latter that we needed to implement the function.

Let us make this counting logic even more general. Perhaps we would like to know how many values in an array of percentages are greater than ninety. Or, how many values in an array of Cartesian points are inside a circle of radius of 1.0 centered on the origin. To accomplish these tasks, we need to replace the equality test in the if statement with a test for some other property. To accomplish this task, we make use of generic formal subprograms. As our last