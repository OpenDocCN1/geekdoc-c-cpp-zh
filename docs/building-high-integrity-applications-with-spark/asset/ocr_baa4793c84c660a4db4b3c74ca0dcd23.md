A_Pack. The body of package A_Pack refines the abstract state State into the concrete variable Total, which is used in the Refined_Global and Refined_Depends aspects of procedure A_Proc.

We could easily extend the logic illustrated by this example with additional abstract states in packages nested within the body of Hierarchical_State_Demo (to widen our hierarchy) or with packages nested within the body of package A_Pack (to deepen our hierarchy). The obvious problem with these extensions is that the package body Hierarchical_State_Demo grows larger with each additional state abstraction.

A seemingly obvious answer to this problem is to put the nested package into an independent library unit and use a with clause to gain access to it. Here is a version of Hierarchical_State_Demo that does just that:

```
with Hierarchical_State_Demo.A_Pack;
package body Hierarchical_State_Demo -- Child package implementation
   with SPARK_Mode => On,
        Refined_State => (Top_State => (Count, A_Pack.State))
is
   Count : Natural := 0;

   procedure Do_Something (Value   : in out Natural;
                           Success :    out Boolean)
     with Refined_Global  => (In_Out => (Count, A_Pack.State)),
          Refined_Depends => (Value   =>+ (Count, A_Pack.State),
                              Success => (Value, Count, A_Pack.State),
                              Count   =>+ null,
                              A_Pack.State =>+ (Count, Value)) is
   begin
      . . . . .
   end Do_Something;
end Hierarchical_State_Demo;
```

Removing the nested package A_Pack has made this body much shorter. We made A_Pack a child of Hierarchical_State_Demo to align our package hierarchy with our abstract state hierarchy.

However, we run into difficulty when we attempt to examine the independent child package containing our new abstract state. SPARK requires that all refined states be hidden from clients—in our example, the clients of Hierarchical_State_Demo. This was not a problem when the package with the abstract state used in the refinement was nested in the body. But as an ordinary child package, it is accessible to all.