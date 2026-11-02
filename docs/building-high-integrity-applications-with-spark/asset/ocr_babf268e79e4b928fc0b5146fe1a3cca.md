the assertions to prove that they, along with the rest of the program, are free of runtime errors.

If the assertion is possibly false or outright illogical, it is appropriate for the tools to object to it. However, there are situations in which an assertion is mathematically true and yet causes runtime errors when evaluated. There is only one way that can happen: arithmetic overflow. If the assertion contains other kinds of runtime errors such as division by zero or accessing an array out of bounds, the assertion does not make sense anyway.

As an example, consider the following silly procedure with a precondition that expresses a true fact about the parameters:

```
```pascal
procedure Silly (X      : in  Positive ;
                 Y      : in  Positive ;
                 Result : out Positive )
with
  Pre => ((X + Y) / 2 in Positive)
is
begin
  if X > 10 then
    Result := 1;
  else
    Result := Y / 2 + 1;
  end if;
end Silly ;
```
```

The precondition asserts that the average of the two Positive parameters is in the range of Positive and then does some pointless computations that nevertheless are completely free of runtime error and obey the synthesized flow dependency contract. There is nothing wrong with this procedure, yet the evaluation of the precondition may raise Constraint_Error because X + Y might overflow the base type of Positive. The SPARK tools will generate an unprovable verification condition attempting to check that overflow will not occur.

One way to work around this is to write the assertions carefully so that they too will be free of runtime error. However, you may feel frustrated by this, particularly if you plan to deploy your program with assertion checking disabled, as we discuss in Section 6.8. The assertions are, after all, intended to be statements about the design of your system. Why can they not be evaluated in the pure mathematical world where concerns about machine limitations do not exist?