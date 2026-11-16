• We must be careful not to include terms with 0 coefficient in the sum. For example:

```
6X^5 + 2X^4 + 3X^3 + 2X
+
3X^5 - 2X^4 - 5X^2 - 8X + 7
9X^5 + 3X^4 - 5X^4 - 6X + 7
```

```
// poly.c

#include <stdio.h>

typedef struct poly {
    float coeff;
    int expo;
    struct poly *next;
} *POLYPTR;

POLYPTR sum(POLYPTR p, POLYPTR q) {
    float coeff;
    POLYPTR add = NULL;

    while (p != NULL && q != NULL) {
        if (p->expon == q->expon) {
            coeff = p->coeff + q->coeff;
            if (coeff) {
                makeTerm(sadd, coeff, p->expon);
                p = p->next;
                q = q->next;
            }
        }
        else if (p->expon > q->expon) {
            makeTerm(sadd, p->coeff, p->expon);
            p = p->next;
        }
        else {
            makeTerm(sadd, q->coeff, q->expon);
            q = q->next;
        }
    }

    while (p) {
        makeTerm(sadd, p->coeff, p->expon);
        p = p->next;
    }

    while (q) {
        makeTerm(sadd, q->coeff, q->expon);
        q = q->next;
    }

    return add;
}
```