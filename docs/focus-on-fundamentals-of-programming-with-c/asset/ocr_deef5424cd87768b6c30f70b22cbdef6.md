# # Storage Location

C divides memory into four separate locations Stack, Heap, Data Area, Code Area.

# ## High Memory

| Component | Details |
|---|---|
| Stack | (changes size freely)\n• C maintains stack for us\n• automatic variables\n• pass parameters to functions\n• store return addresses\n• set up at top of available memory and grows towards lower memory as it is filled |
| Heap | (changes size freely)\n• allocating and using memory on heap\n• is our responsibility (malloc)\n• starts in low memory and grows towards higher memory |
| Data Area | (fixed in size)\n• Uninitialized data\n• uninitialized static and external variables\n• all initialized to zero at once\n• Initialized data\n• initialized static and external variables\n• initialized arrays and structures |
| Code Area | (fixed in size)\n• program code\n• not changed when program runs |

# ## Low Memory