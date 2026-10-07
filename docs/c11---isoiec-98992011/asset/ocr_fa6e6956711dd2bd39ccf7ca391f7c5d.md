# ISO/IEC 9899:2011 (E)  © ISO/IEC 2011 – All rights reserved

# 7.22.2 Pseudo-random sequence generation functions

# 7.22.2.1 The rand function

Synopsis

```
#include <stdlib.h>
int rand(void);
```

Description

The rand function computes a sequence of pseudo-random integers in the range 0 to RAND_MAX<sup>295</sup>

The rand function is not required to avoid data races with other calls to pseudo-random sequence generation functions. The implementation shall behave as if no library function calls as the rand function.

Returns

The rand function returns a pseudo-random integer.

Environmental limits

The value of the RAND_MAX macro shall be at least 32677.

# 7.22.2.2 The srand function

Synopsis

```
#include <stdlib.h>
void srand(unsigned int seed);
```

Description

The srand function uses the argument as a seed for a new sequence of pseudo-random numbers to be returned by subsequent calls to rand. If srand is called with the same seed value the sequence of pseudo-random numbers shall be repeated. If rand is called before any calls to srand have been made, the same sequence shall be generated as when srand is first called with a seed value of 1.

The srand function is not required to avoid data races with other calls to pseudo-random sequence generation functions. The implementation shall behave as if no library function calls as the srand function.

295 There are no guarantees as to the quality of the random sequence produced and some implementations are known to produce sequences with distractingly non-random low-order bits. Applications with particular requirements use a generator that is known to be sufficient for their needs.

346 Library 7.22.2.2