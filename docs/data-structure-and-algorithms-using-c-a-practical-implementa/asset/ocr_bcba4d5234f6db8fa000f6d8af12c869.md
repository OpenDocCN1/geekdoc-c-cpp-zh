```
ELSE:
NODE := NEXT[NODE]
COUNT := COUNT+1
[END OF IF]
[END OF LOOP]
STEP-4 : RETURN
```

```
ALGORITHM FOR INSERTION OF A NODE WHEN INFORMATION IS KNOWN
INSINFO(START,NODE,VAL)
STEP-1 : NODE := NEXT[START]
STEP-2 : REPEAT WHILE [NEXT[NODE]!=[NULL]
IF(INFO[NODE] = VAL) THEN:
    WRITE : INFO[NODE]
    NEXT[PREV[NODE]] := NEXT[NODE]
    PREV[NEXT[NODE]] := PREV[NODE]
    FREE(NODE)
ELSE:
    NODE := NEXT[NODE]
[END OF IF]
[END OF LOOP]
STEP-3 : RETURN
```

# 7.6 Programs on Double Linked List

# 7.6.1 /* Creation of Double Linked List */

```
#include <iostream>
#include<iostream>
# include <stdlib.h>
using namespace std;
struct link
{
int info;
struct link *next;
struct link *previous;
};
struct link start;
void create (struct link *);
void display (struct link *);
```