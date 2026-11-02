loop in an embedded temperature controller. It obtains the current temperature from an analog-to-digital converter (ADC) and adjusts the output of a gas valve via a digital-to-analog converter (DAC).

```
loop
    ADC.Read (Temperature);      -- Read the temperature from the ADC
    Calculate_Valve (Current_Temp => Temperature,  -- Calculate the new
                     New_Setting => Valve.Setting); -- gas valve setting
    DAC.Write (Valve_Setting);      -- Change the gas valve setting
end loop;
```

We use an exit statement within a loop to terminate the execution of that loop when some condition is met. The exit statement may go anywhere in the sequence of statements making up the loop body. A loop that reads and sums integer values until it encounters a negative sentinel value follows. The negative value is not added to the sum.

```
Sum := 0;
loop
    Ada.Integer_Text_IO.Get (Value);
    exit when Value < 0;
    Sum := Sum + Value;
end loop;
```

There are two iteration schemes that may be used with the loop statement. The while iteration scheme is used to create a pretest loop. The loop body is executed while the condition is true. The loop terminates when the condition is false. The following loop uses a while iteration scheme to calculate an approximation of the square root of X using Newton’s method.

```
Approx := X / 2.0;
while abs (X - Approx ** 2) > Tolerance loop
    Approx := 0.5 * (Approx + X / Approx);
end loop;
```

This program fragment uses two operators not found in some programming languages. The operator abs returns the absolute value of its operand, and ** is used to raise a number to an integer power.

The for iteration scheme is used to create deterministic counting loops. A simple example of this scheme is as follows.

```
for Count in Integer range 5 .. 8 loop
    Ada.Integer_Text_IO.Put (Count);
end loop;
```