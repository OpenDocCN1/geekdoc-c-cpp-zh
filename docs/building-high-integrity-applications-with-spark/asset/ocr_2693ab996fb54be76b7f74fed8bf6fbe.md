```
```ada
Positive range 1 .. Maximum_Description_Length;
subtype Description_Count_Type is
   Natural range 0 .. Maximum_Description_Length;
subtype Description_Type is String(Description_Index_Type);

-- Each Event_Record handles exactly one datebook entry.
type Event_Record is
   record
      Description_Text : Description_Type;
      Description_Size : Description_Count_Type;
      Date             : Dates.Datetime;
      Is_Used          : Boolean;
   end record;

subtype Event_Index_Type is
   Positive range 1 .. Maximum_Number_Of_Events;
type Datebook is
   array (Event_Index_Type) of Event_Record;

end Datebooks;
```
```

In this version the caller must create a Datebook object and explicitly pass it to the various subprograms in the package. Accordingly, those subprograms, such as Add_Event, must now be given an additional parameter. The subprograms no longer have a data dependency contract, but the flow dependency contract appropriate for the new parameter mimics the flow dependency contract used with the state abstraction in the original version of the package.

This version has some advantages over the previous version. First, it allows clients to create and manipulate many different Datebook objects. Second, package Datebooks has no internal state, which presents advantages in multi-tasking environments. However, the original version was easier to use because clients did not need to create their own datebooks. The most appropriate approach depends on the application’s needs.

The private section, shown in full earlier, seems complicated. However, the original Datebook package needs similar declarations in the package body to fully define the internal state of that package. This is described in more detail in the next section.

# 4.3.1 *Refinement*

When a state abstraction is used, the body of the package must explicitly declare which global variables and nested package state, if any, compose the abstract