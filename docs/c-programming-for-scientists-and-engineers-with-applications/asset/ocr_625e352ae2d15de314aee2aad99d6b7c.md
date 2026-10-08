# Method

Input the names into a list.
Output the unsorted names.
Sort the names in alphabetical order.
Output the sorted names.

# Data

Input 11 names.

# Pseudocode

```
main:
  call funcinput
  call funcsort
  call funcoutput
stop
funcinput:
  for each name
    input the name
  end for
return
end
funcsort:
  for each name i
    for each name j j > i
      if ( name j should be followed by name i)
        swap the names
      end if
    end for
end for
end
```