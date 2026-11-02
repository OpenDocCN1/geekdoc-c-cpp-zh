# 2.4.2 Generic Subprograms

Ada provides parameterized generic units for writing reusable software components. Generic units are templates that can be instantiated to create a unit for a specific application. While the initial effort to create a generic unit may be higher, the long-term savings can be substantial. Not only can we reuse the code in the template, but also we need only test one instance to verify all future instantiations.⁴ We have already seen how to use generic packages to create packages for doing input and output with the types we define. Now let us look at writing our own generic units.

Suppose we have written the following function to count the number of times a particular character occurs in a string of characters:

```
function Count (Source : in String;
    Pattern : in Character) return Natural is
  -- Returns the number of times Pattern occurs in Source
  Result : Natural := 0;
begin
  for Index in Source'Range loop
    if Source (Index) = Pattern then
      Result := Result + 1;
    end if;
  end loop;
  return Result;
end Count;
```

While this function is specific for counting characters in a string, the same logic could be used for counting occurrences of objects in any array. For each different application we need different types for the parameters Source and Pattern. Rather than write a new counting function for each application, we can write a single generic function and instantiate it as appropriate. We supply the different types for each application through generic parameters. We define generic formal parameters in the specification of the generic unit and supply generic actual parameters when we instantiate the generic unit for a particular application. Ada provides many different kinds of generic formal parameters with specific rules for what actual parameters may be supplied. Table 2.2 shows the commonly used generic formal types with descriptions of what generic actual types are acceptable. See the ARM (2012), Barnes (2014), or Wikibooks (2014) for a complete list.

Let us start with our type for Pattern. This type is also the type of the components in the array we wish to process. There are no restrictions on what