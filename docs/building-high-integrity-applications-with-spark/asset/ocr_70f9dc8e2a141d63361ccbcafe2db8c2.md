```
~~~ada
procedure Big_Search is
    new Searchers.Binary_Search (Element_Type => Big_Integer,
                                 Index_Type   => Index_Type,
                                 Array_Type   => Big_Array_Type,
                                 "<"          => Very_Longs."<");
~~~
```

In this case the elements of the array are 256-bit integers. Notice that because the "<" operator of the Very_Long type is not directly visible, it must be explicitly named as a generic argument in the instantiation.

Unlike the earlier case, the SPARK tools have no built-in knowledge of the behavior of "<" for the Very_Long type. All they know about the operator is what they learn from the contract on the operator function provided by the package. That contract does not completely specify all the relevant properties of Very_Longs."<", and thus the tools may have more difficulties with the proofs for this instantiation. The necessary properties can be provided to the SPARK tools using an *external axiomatization*, an advanced technique we discuss very briefly in Section 9.4. However, this example shows the value of analyzing each instantiation separately. The tools are able to take advantage of whatever specific information is available for each instantiation. If the tools attempted to prove the generic once and for all, they would not be able to use specialized information to simplify the proofs when appropriate.

Let us now turn our attention to the pre- and postconditions on Binary_Search, repeated here as a convenience.

```
~~~ada
Pre =>
  (for all J in Items'Range =>
    (for all K in J + 1 .. Items'Last => Items (J) < Items (K))),
Post =>
  (if Found then
    Search_Item = Items(Result)
  else
    (for all J in Items'Range => Items (J) /= Search_Item));
~~~
```

The precondition is similar to the one given for the nongeneric version of the procedure described in Section 6.2.1. In particular, it asserts that the input array is sorted and also, in this case, that every element in the array is unique. Be aware, however, that such a conclusion relies on the “expected” properties of "<". While there is nothing in the generic code itself that guarantees "<" behaves as expected, the SPARK tools will use whatever interpretation is justified at the point of instantiation as described previously.

It might seem more natural and more general to use "<=" in the precondition as was done in the nongeneric example. Unfortunately, no "<=" operator is