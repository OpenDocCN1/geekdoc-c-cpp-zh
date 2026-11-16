# Storage Location

C divides memory into four separate locations: Stack, Heap, Data Area, Code Area.

# High Memory

| Memory Location | Details |
| :--- | :--- |
| **Stack** (changes size freely) | • C maintains stack for us
• automatic variables
• pass parameters to functions
• store return addresses
• set up at top of available memory and grows towards lower memory as it is filled |
| | (Arrows indicating growth direction) |
| **Heap** (changes size freely) | • allocating and using memory on heap
• is our responsibility (malloc)
• starts in low memory and grows towards higher memory |
| **Data Area** (fixed in size) | Uninitialized data
• uninitialized static and external variables
• all initialized to zero at once

Initialized data
• initialized static and external variables
• initialized arrays and structures |
| **Code Area** (fixed in size) | • program code
• not changed when program runs |

# Low Memory