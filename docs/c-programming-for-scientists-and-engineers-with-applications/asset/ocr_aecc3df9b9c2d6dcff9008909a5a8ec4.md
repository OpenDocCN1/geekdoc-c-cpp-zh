# Section 10.2.3

+   1. a. true
   b. false
   c. true
   d. false
   e. true

+   2. a. int *ptr;
   ptr = 2; /* causes error */
   b. int *ptr1, *ptr2, *ptr3;
   int x[5] = {1, 2, 3, 4, 5};
   ptr1 = x;
   ptr2 = x;
   ptr3 = ptr1 + ptr2; /* causes an error */
   c. int *ptr1, *ptr2, *ptr3;
   int x[5] = {1, 2, 3, 4, 5};
   ptr1 = x;
   ptr2 = x;
   ptr3 = ptr1 - ptr2; /* permissible but to use ptr3 */
   d. int a[3], b[3];/* would cause an error */
   int *ptra;
   ptra = a;
   b = a;
   a = a + ptra; /* causes an error */
   e. int x;
   int *ptr1, *ptr2;
   ptr1 = &x;
   ptr2 = &x;

# Section 10.3.4

+   1. a. false
   b. true
   c. true
   d. false