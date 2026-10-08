# 7.01 Short Answer Poll

What are the final values of the index variables after the following DO statements execute?

```
do i=1 to 5;
end;
do j=2 to 8 by 2;
...
end;
do k=10 to 2 by -2;
...
end;
```

The final value is highlighted.
1 2 3 4 5 6
24 68 10
1086420

# Sample DO Loops with Item Lists

+   - The DO loop is executed once for each item in the list.
- The list must be comma separated.

```
do Month='JAN', 'FEB', 'MAR';
...
end;
doo odd=1,3,5,7,9;
end;
do i=Var1,Var2,Var3;
...
DO index-variable=item-1<...item-n>;
```

Enclose character constants in quotation marks.