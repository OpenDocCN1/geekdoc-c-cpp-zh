```
is
  type Status_Type is (Success, Description_Too_Long, Insufficient_Space);

  procedure Initialize
    with
      Global => (Output => (Book, Index)),
      Depends => (((Book, Index) => null));

  procedure Compact_Index
    with
      Global => (In_Out => Index),
      Depends => (Index =>+ null);

  procedure Add_Event (Description : in String;
                        Date : in Dates.Datetime;
                        Status : out Status_Type)
    with
      Global => (In_Out => (Book, Index)),
      Depends => (Book =>+ (Description, Date),
                  Index =>+ (Description, Date),
                  Status => (Description , Book));

end Indexed_Datebook_V2;
```

In addition to declaring two state abstractions, the package declares that one of those abstractions is automatically initialized. The data and flow dependency contracts on procedure Compact_Index indicate that it only needs the Index abstraction to be initialized before it can be used. Flow analysis will now allow Compact_Index to be called before Initialize is called.

The body of package Indexed_Datebook needs to also show how each state abstraction is refined. For example,

```
package body Datebook
  with
    Refined_State => (Book => Event_Array,
                      Index => Event_Index)
is
  ...
end Datebook;
```

The refined aspects on the subprogram bodies remain as before because they were written in terms of the constituents anyway. Flow analysis will verify, of course, that the refined contracts on the bodies are consistent with the contracts in the declarations of the subprograms.