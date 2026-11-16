# Storage Location

C divides memory into four separate locations: Stack, Heap, Data Area, Code Area.

# High Memory

| Section | Content |
| --- | --- |
| **Stack** (changes size freely) | * C maintains stack for us<br>* automatic variables<br>* pass parameters to functions<br>* store return addresses<br>* set up at top of available memory and grows towards lower memory as it is filled |
| | v<br>^ |
| **Heap** (changes size freely) | * allocating and using memory on heap is our responsibility (malloc)<br>* starts in low memory and grows towards higher memory |
| **Data Area** (fixed in size) | * Uninitialized data<br>* uninitialized static and external variables<br>* all initialized to zero at once<br>--<br>* Initialized data<br>* initialized static and external variables<br>* initialized arrays and structures |
| **Code Area** (fixed in size) | * program code<br>* not changed when program runs |

# Low Memory