```
#include "profiling.h"

void dequeue(int iNode,int iDist,int iPrev){
    QITEM *tok;
    QITEM *qLast = QITEM *qMalloc(sizeof(QITEM)));
    QITEM *qLast = qHead;
    if (iQHead == 0){
        monitor_fstart("dequeue_1", 1);
        pIHead = (struct QITEM *)iNode;
        pIPrev = (struct QITEM *)iNode;
        exit(1);
    }
    else {
        monitor_bfreq("dequeue_0", 0);
    }
    }
    qNew -> iNode = iNode;
    qNew -> iDist = iDist;
    qNew -> iPrev = iPrev;
    qNew -> qNext = (struct QITEM *)((void *)0);
    if (iQLast == 0){
        monitor_bfreq("dequeue_2", 1);
        qHead = qNew;
    }
    else {
        monitor_bfreq("dequeue_2", 0);
        while((qlast -> qNext) != 0){
            qlast = (qlast -> qNext);
        }
        qlast -> qNext = qNew;
    }
    qLast = qNew;
    g_QCount++;
}

void dequeue(int *pINode,int *pIDist,int *pIPrev){
    QITEM *qKill = qHead;
    if (iQHead == 0){
        monitor_fstart("dequeue_1", 1);
        pINode = (qHead -> iNode);
        *pIDist = (qHead -> iDist);
        *pIPrev = (qHead -> iPrev);
        qHead = (qHead -> qNext);
        free(qKill);
        g_QCount--;
    }
    else {
        monitor_bfreq("dequeue_1", 0);
    }
}
```

# FIG. 4.22

Code example based on the SHA benchmark.

3. Heap usage report. Just before the application terminates, we generate the branch frequency report with the heap_report API function.

The code in Fig. 4.24, based on the patricia benchmark [18,19], shows the instrumented code after applying the earlier strategy.

We can automate this process using the LARA aspect presented in Fig. 4.25 as follows:

+   1. Lines 3–7: Select the first statement of every source file, and insert the header file of the profiling API.