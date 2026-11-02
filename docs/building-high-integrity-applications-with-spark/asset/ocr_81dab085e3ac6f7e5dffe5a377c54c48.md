```
type Percent    is delta 0.25 range 0.0 .. 100.0;
type Percent_Array is array ( Integer range <> ) of Percent;

function Num_Below (List  : in Percent_Array;
                    Value : in Percent) return Natural
-- Returns the number of values in List that are less than Value
with
    Pre => (

is
    Result : Natural;
    Index  : Integer;
begin
    Result := 0;
    Index  := List' First ;
loop
    exit when Index > List'Last or else List (Index) >= Value;
    Result := Result + 1;
    Index  := Index + 1;
end loop;
    return Result;
end Num_Below;
```

5.14 Add a second precondition to the function in Exercise 5.13 that states that List contains at least one value.