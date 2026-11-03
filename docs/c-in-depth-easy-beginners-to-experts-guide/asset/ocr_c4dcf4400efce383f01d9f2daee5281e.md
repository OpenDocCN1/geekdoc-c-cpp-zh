# (C) HEAVY USE OF typedef.

# 1. SIZE OF POINTERS:

You must know that window permits multiple programs to coexist in memory at that time it needs powerful 32-bit microprocessor to execute these programs and simple memory to house them. Whenever we store a value at a memory location the address of this memory location has to be stored first in the c.p.u register at the same point in time.

And one most thing the Amount of memory that a microprocessor can access depends on the size of the cpu registers. This means we can store 232 unique addresses in the cpu registers at different times, as a result, we can access 4 GB memory locations using 32-bit registers. In our programs the 32 bit address have to be stored in pointers,do not forget that every pointer under 32-bit environment is a 4 byte entity.

# 2. SIZE OF INTEGERS:

I wanna to tell u that in 16 bit environment the size of integer is of 2 bytes, in the other hand in 32 bit environment the size of the interger is of 4 bytes. After 32 bit the range of interger is going to be -2147483648 to +2147483647. By this u think there is know difference between int and long int, but what if we wish to store age of person? And we know that age is going to be hardly 100,in such case its best to use short int. 3

# 3. HEAVY USE OF typedef:

If I write the following declairations--

```
HANDLE h;
WAPRAM w;
LPARAM I;
```

Is theae are the data types?
No, they are typedef's okay.
Why c program under windows used heavily typedef?
Its have a 2 reasons!!

# (A)

A typical window program is required to perform several complex tasks for ex:- print documents, send mails, performing i/o , managing multiple threads , data processing tasks etc. all of these used to need integers. But if we use normal interger