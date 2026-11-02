```
~~~ada
Data_Size  : in   Data_Size_Type;
Stop       : in   Stop_Type;
Status     : out Status_Type)
with
   Global  => (In_Out => Port_State),
   Depends => ((Port_State, Status) =>
                 (Port_State, Baud, Parity, Data_Size, Stop));

-- Returns IO_Failure if port is not open or if the underlying I/O fails.
procedure Read (Item   : out Byte;
                Status : out Status_Type)
  with
    Global  => (Input => (Port_State, Data_State)),
    Depends => (Item => (Port_State, Data_State), Status => Port_State);

-- Returns IO_Failure if port is not open or if the underlying I/O fails.
procedure Write (Item   : in  Byte;
                 Status : out Status_Type)
  with
    Global  => (Input => Port_State, Output => Data_State),
    Depends => (Data_State => (Port_State, Item), Status => Port_State);

-- Has no effect if port is not open. Returns no failure indication.
procedure Close
  with
    Global  => (In_Out => Port_State),
    Depends => (Port_State => Port_State);
end Serial_Port ;
~~~
```

The specification of the package is in SPARK and declares two state abstractions. The first, Port_State, models the serial port hardware itself. It tracks if the port is open, the serial parameters that are in use and any other related information such as permissions or system level errors. This state is initialized in some way by the underlying system so the package declares that Port_State is automatically initialized.

The other state abstraction, Data_State, represents the external subsystem to which the serial port is connected and is thus declared to be an external state abstraction. Because none of the four external properties are specified, they all default to true. The external subsystem is assumed to do I/O asynchronously with the serial port and that, furthermore, all reads and writes to the port are effective. In particular, two successive reads from the port may return different values, and writing the same value to the port twice in succession is certainly useful.