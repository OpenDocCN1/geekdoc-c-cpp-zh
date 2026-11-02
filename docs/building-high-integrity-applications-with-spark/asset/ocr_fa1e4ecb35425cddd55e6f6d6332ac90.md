```
procedure Get_Line (Buffer  : out String;
    Count  : out Natural;
    Status : out Status_Type)
with
  Global => (Input => (Serial_Port.Port_State,
      Serial_Port.Data_State)),
  Depends => ((Buffer, Count, Status) => (Buffer,
      Serial_Port.Port_State,
      Serial_Port.Data_State));
end Terminal;
```

This specification only shows a single procedure, Get_Line, that reads a carriage return terminated string of characters from the terminal and installs them into the given buffer. It returns an error indication if it runs out of space before getting a carriage return character or if the underlying serial port reports an I/O error.

The procedure is decorated with SPARK data and flow dependency contracts written in terms of the state abstractions of the underlying serial port. This appears to be a violation of information hiding: the specification otherwise does not mention the serial port at all, leading one to suppose that it could support other kinds of communications media.

However, despite syntactic appearances, the use of the serial port is not hidden by this package. For example, it is important to open the serial port before calling Get_Line; the dependency of Get_Line on the port state must be declared. Thus, SPARK serves to make explicitly visible dependencies that are semantically visible in any case.

The body of package Terminal is straight forward and shown here in its entirety:

```
with Ada.Characters.Latin_1;
package body Terminal
  with Spark_Mode => On
is
  use type Serial.Port.Status_Type;

  procedure Get_Line (Buffer : out String;
      Count : out Natural;
      Status : out Status_Type) is
    Value : Serial.Port.Byte;
    Port_Status : Serial.Port.Status_Type;
  begin
    Buffer := (others => ' ');
    Count := 0;
    Status := Success;
```