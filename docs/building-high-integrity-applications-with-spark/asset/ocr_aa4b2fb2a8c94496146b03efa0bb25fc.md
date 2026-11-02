As an example, consider an embedded system using a 64-bit counter as a kind of clock. The following procedure Tick is called each millisecond to update the clock value and do other housekeeping:

```
```ada
pragma SPARK_Mode(On);
package body TickTock
   with Refined_State => (TickTock_State => Clock_Value)
is
   type Clock_Type is range 0 .. 2 ** 63 - 1;
   Clock_Value : Clock_Type := 0;

   procedure Tick
     with
       Refined_Global  => (In_Out => Clock_Value),
       Refined_Depends => (Clock_Value =>+ null)
   is
   begin
      Clock_Value := Clock_Value + 1;
      -- Other housekeeping...
   end Tick;

end TickTock;
```
```

In this simple program, the SPARK tools cannot prove the incrementing of Clock_Value will stay in range. However, if the system initializes at boot time and increments Clock_Value only once every millisecond, it would take more than 290 million years to reach its maximum value.

You could push the proofs through by adding error handling:

```
```ada
if Clock_Value = Clock_Type'Last then
   Restart_System;
else
   Clock_Value := Clock_Value + 1;
end if;
```
```

In the event that the system is still running when the next supercontinent forms, it now has the sense to reboot and re-initialize itself. More importantly, the SPARK tools are now convinced that Clock_Value + 1 is safe. However, adding error handling like this for a condition that will never arise in any realistic scenario is more obscure than useful.

Instead, this is an appropriate place to use Assume:

```
```ada
pragma Assume (Clock_Value < Clock_Type'Last);
Clock_Value := Clock_Value + 1;
```
```