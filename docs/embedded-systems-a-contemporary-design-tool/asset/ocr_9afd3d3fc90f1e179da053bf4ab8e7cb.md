(e) Execute the architectural design. Map each of the functions onto the hardware and software.

+   1. Design an automatic coffee pot with the following capabilities.
+      The controls must include the ability to set the start time on a 24-hour clock, reduce the temperature to warming and annunciate when the brew cycle is complete, and stop water flow if the pot is removed from its receptacle.
+   
+   2. Design a digital watch with the following capabilities.
+      The controls must include 12-hour time expressed in hours, minutes, and seconds, AM and PM tracking and annunciation, alarm, and the ability to set the alarm and time values.
+   
+   3. Design a washing machine with the following capabilities.
+      The controls must include the ability to set water temperature, washing start times, modes (presoak, normal, permanent press, delicate), and annunciation of temperature, times, and mode.
+   
+   4. Design an automatic oven control with the following capabilities.
+      The controls must include the ability to set temperatures, cooking start and stop times, modes (bake, broil, clean), and annunciation of temperature, times, and mode.
+   
+   5. Design a module implementing a four-seat passenger entertainment system with the following capabilities on a commercial aircraft.
+      The entertainment system should support the ability for each of the four passengers to program and control:
+      - Movie selection
+      - Audio selection
+      - A gaming console.
+   
+   6. Design a seat belt-engine-door lock interlock with the following capabilities.
+      The engine cannot start if the seat belt is not fastened. The doors automatically lock when the engine is started.
+   
+   7. Design a new toy bank that we see in Figure P9.1.

![](bbox=[0.2, 0.65, 0.38, 0.75])

# Figure P9.1

The toy is intended to let children have fun while learning to save money.
When the child puts in 0 or 2 coins – pennies, nickels, dimes, or quarters – the ODDLY eye will flash according to how much money was put in. If the little one puts in 1 or 3 coins, the EVENLY eye will similarly flash.

8. A new temperature monitoring system that utilizes an analog-to-digital converter to collect data at various points in a yogurt production process is to be designed. The control logic accepts the input signals shown and generates the output signals as specified in Figure P9.2.

![](bbox=[0.55, 0.16, 0.85, 0.24])

# Figure P9.2

Upon receipt of a start signal, the system must cycle through the three time intervals – t1, t2, and t3 - and command the following operations to take place: Sample, Convert, and Autozero. The system is to respond to the input signals as shown in the diagram. At the end of time t3, as signaled by the Tend input, the system must return to its initial state and wait for a start input.
The times, t1-t3, are not inputs to the system; they merely identify the length of each interval.
The signals start, done, and Tend are inputs to the system. They identify the start or end of the intervals as indicated.
The system must have several output signals to control the electronics doing the conversion. The control logic is one room, and the analog-to-digital converter is in another. There is a limit to the number of wires in the cable connecting the two portions of the system.
The system must accept analog signals from eight different points around the tank where the yogurt is fermenting.

9. You have been hired by Let There Be Lyght – Signs Abound, Ltd. to design a traffic control system. The design your predecessor proposed failed at a critical time while he was in the middle of the intersection testing it. The intersection you must control is shown in Figure P9.3. Your design must meet the following specifications:

![](bbox=[0.6, 0.66, 0.8, 0.8])

# Figure P9.3

+   (a) Each light, L1 and L2, has two states, ON or OFF.
+   (b) If a car arrives at the intersection and the light in its direction is OFF, it may proceed through the intersection.