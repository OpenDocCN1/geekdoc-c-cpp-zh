
a special end-of-list element, also called a *sentinel* element, that conceptually exists just past the last valid element. The Back function returns an iterator to the sentinel; it is valid to call Back even for an empty list.

A more complete package would also include subprograms for moving iterators forward and backward over the list and for reading and writing list items through iterators. The generic parameter Default_Element is intended to be returned when one attempts to (incorrectly) read the list’s sentinel. The generic package cannot know what value would be appropriate to return in that case so it relies on the instantiation to provide such a value.

The package specification has SPARK data and flow dependency contracts and a declaration of the abstract state held by the package. Here is the body of this abbreviated package:

```ada
package body Double_List
with
   Refined_State => (Internal_List => (Memory, Count, Free_List, Free))
is

   subtype Index_Type is Iterator ;

   type List_Node is
      record
         Value    : Element_Type;
         Next     : Index_Type;
         Previous : Index_Type;
      end record;

   type Node_Array is array (Index_Type) of List_Node;
   type Free_Array is array (Index_Type) of Index_Type;

   Memory    : Node_Array; -- Holds the list nodes.
   Count     : Index_Type; -- Number of items on the list.
   Free_List : Free_Array; -- Maps available nodes.
   Free      : Index_Type; -- Points at the head of the free list.

procedure Clear
   with
      Refined_Global  => (Output => (Memory, Count, Free_List, Free)),
      Refined_Depends => ((Memory, Count, Free_List, Free) => null)
is
begin
   -- Make sure the entire array has some appropriate initial value.
   Memory := (others => (Default_Element, 0, 0));
   Count := 0;

   -- Prepare the free list.
   Free_List := (others => 0);
   Free := 1;
   for Index in Index_Type range 1 .. Index_Type'Last - 1 loop
       Free_List (Index) := Index + 1;
   end loop;
end Clear;

procedure Insert_Before (It     : in  Iterator;
                         Item   : in  Element_Type;
                         Status : out Status_Type)
with
    Refined_Global  => (Input => Free_List,
                        In_Out => (Memory, Count, Free)),
    Refined_Depends => (Memory =>+ (Count, It, Item, Free),
                        (Count, Status) => Count,
                        Free            =>+ (Count, Free_List))
is
    New_Pointer : Index_Type;
begin
    if Count = Index_Type(Max_Size) then
        Status := Insufficient_Space;
    else
        Status := Success;

        -- Get an item from the free list.
        New_Pointer := Free;
        Free := Free_List (Free);

        -- Fill in the fields and link the new item into the list.
        Memory(New_Pointer) := (Item, It, Memory(It).Previous);
        Memory(Memory(It).Previous).Next := New_Pointer;
        Memory(It).Previous := New_Pointer;

        -- Adjust count.
        Count := Count + 1;
    end if;
end Insert_Before;

function Back return Iterator is
begin
    return 0;
end Back;

function Size return Natural is (Natural(Count))
  with Refined_Global => (Input => Count);

begin
   -- Clear the list at package elaboration time.
   Clear;
end Double_List;
```

A List_Node type is defined containing a value of the list’s Element_Type along with two “pointers” to the next and previous nodes in the list. Here, the pointers are implemented as indices into a suitably dimensioned array of list nodes. Each list node has a corresponding component in the Free_List array indicating if the node is available or not. The free list itself is a singly linked list with the head given by Free. The list node at position zero is the sentinel node.

The package body also has SPARK aspects as usual, including a refinement of the package’s abstract state and refined data and flow dependency contracts. Although not used in this example, the body may contain other SPARK assertions such as loop invariants needed to prove instantiations of this generic unit.

Despite the SPARK aspects, the SPARK tools do not directly analyze the generic code. Instead, the aspects are used when SPARK analyzes each instantiation. Consider a simple package that provides higher level subprograms around a particular instantiation of a list of integers. For the sake of an example, this package is shown with a single procedure Append_Range that appends a given range of integers onto the list.

```ada
pragma SPARK_Mode(On);
package List_Handler -- To demonstrate instantiation of generic package.
  with
    Abstract_State => List,
    Initializes    => List
is
  procedure Append_Range (Lower, Upper : in Integer)
    with
      Global  => (In_Out => List),
      Depends => (List =>+ (Lower, Upper));
end List_Handler;
```

The package is given a SPARK specification by way of the SPARK_Mode pragma. It declares as abstract state the list it is managing. Here is the body of this package:

```ada
pragma SPARK_Mode(On);
with Double_List; -- The generic doubly linked list package
pragma Elaborate_All(Double_List);

package body List_Handler
with
   Refined_State => (List => Integer_List.Internal_List)
is
   package Integer_List is new Double_List (Element_Type => Integer,
                                             Max_Size => 128,
                                             Default_Element => 0);
   use type Integer_List.Status_Type;

   procedure Append_Range(Lower, Upper : in Integer)
   with
      Refined_Global => (In_Out => Integer_List.Internal_List),
      Refined_Depends => (Integer_List.Internal_List =>+ (Lower, Upper))
   is
      Current : Integer := Lower;
      Status : Integer_List.Status_Type;
   begin
      while Current <= Upper loop
         Integer_List.Insert_Before (It => Integer_List.Back,
                                      Item => Current,
                                      Status => Status);
         exit when Status /= Integer_List.Success or Current = Upper;
         Current := Current + 1;
      end loop;
   end Append_Range;
end List_Handler;
```

Notice the refined state clause at the beginning of this package body. The abstract state List is refined to the abstract state Internal_List of the instantiated package Integer_List. In effect, the instantiation is a kind of global variable inside package List_Handler.

The pragma Elaborate_All(Double_List) that appears at the top of List_Handler’s body controls elaborate order. As we described in Section 3.6, dependencies between packages sometimes require special measures be taken to control the order in which they are elaborated to ensure no unelaborated units are used. Because the instantiation of Double_List occurs as a global variable in the body of a library level package, the SPARK tools require that Double_List’s body, and transitively the bodies of all packages it depends on, be elaborated first. This is the effect of Elaborate_All. This ensures the elaboration of the instantiation succeeds because all library units required by it will be elaborated by then.

As the SPARK tools do flow analysis and generate verification conditions for the body of package List_Handler, they also do flow analysis and generate verification conditions for the particular instantiation of Double_List being used. If the proofs all succeed, as they do for this example, that only implies the proofs for the Integer_List instantiation succeeded. Other instantiations may have failing proofs and, conceivably, may even have serious errors that the Integer_List instantiation does not.

For example, Integer_List is an instantiation of Double_List with a Max_Size of 128 elements. Because the type of Max_Size is Natural, it is possible to instantiate Double_List with a Max_Size of zero. Conceivably that boundary case may contain runtime problems that the non-zero sized case may not contain. If so, the analysis done by the tools will fail for the problematic instantiation while still passing other, better behaved instantiations.

Some instantiations might not even be SPARK. Consider an instantiation such as

```ada
type Integer_Access is access Integer;
package Integer_Pointer_List is
    new Double_List (Element_Type     => Integer_Access,
                     Max_Size         => 128,
                     Default_Element  => null);
```

This instantiation creates a list variable that holds integer access values. However, because access types are not allowed in SPARK, this instantiation can not appear in code where SPARK_Mode is on. It is not SPARK.

Double_List is a generic variable package. When we instantiate an actual package from it, that instance implements a single list variable. Because it is generic, it can be instantiated multiple times in a program. Thus, our generic variable package supports the creation of multiple list variables. However, the SPARK tools will repeat the proofs for each instantiation. Also, the “variables” created in this way cannot readily be copied or compared as they have, in effect, different types.

An alternative design would be to revise Double_List into a type package that is generic only in the list’s element type. One could use a discriminant on the list type to specify the maximum size of each list object at declaration time. This approach has the advantage of allowing list objects to be assigned and compared provided they had the same size (and the SPARK tools would statically prove that was so). It would also mean the tools would only need to prove the Double_List code once for each element type and not once for each list variable. We leave the details of this alternative design as an exercise for the reader.
