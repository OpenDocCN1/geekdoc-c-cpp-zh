way of explicitly saying that its code is not subject to proof. The Network.Helpers package is now

```
```ada
with Network.Bit_Operations;
use  Network.Bit_Operations;
package body Network.Helpers
  with SPARK_Mode => On
is
  procedure Split16 (Value : in  Double_Octet;
                     MSB   : out Octet;
                     LSB   : out Octet) is
  begin
    MSB := TakeMSB_From16 (Value);
    LSB := TakeLSB_From16 (Value);
  end Split16;
end Network.Helpers;
```
```

This new version proves easily as all the types match without conversions.
Notice that Network.Bit_Operations is a private child package. This is stated by the use of **private** in its specification. Private children are commonly used in Ada as a way of factoring out internal support facilities from a collection of related packages. See Section 3.5.1 for more information. Here we use a private child to encapsulate the unprovable code needed by some other package(s) allowing the bulk of the code base to be proved cleanly.

# ### 9.3.6 When All Else Fails

If you are completely unable to get a verification condition to prove after trying the techniques described in this section, you can instead resort to testing to explore the issue. We discuss this in Section 8.4. Here, the value of SPARK is in the focus it provides. The unproved verification conditions must be carefully covered by test cases, whereas tests to cover the proved aspects of the code are less critical and can be given a lower priority –

+   - Use testing to cover unproved verification conditions.

# ## 9.4 SPARK Internals

In this section we give an overview of how the SPARK tools work internally. Our intention is not to provide a detailed description of the theory and operation of the tools, but rather to give you a sense of what they are doing so you can be a