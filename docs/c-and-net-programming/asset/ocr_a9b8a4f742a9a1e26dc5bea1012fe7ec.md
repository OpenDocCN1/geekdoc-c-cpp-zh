```
{
    // do some local cleanup
    throw ex;
}
```

So basically the Throw exception overwrites the stack trace and this makes it hard to find the original code line number that has thrown the exception. In turn Throw retains the stack information and adds to the stack information in the exception that it is thrown.

# Long Answered Questions

+   Q.1 What are generations in memory management ? (Refer section 13.1)
+   Q.2 Discuss GC in .NET environment. (Refer section 13.1)
+   Q.3 What are exceptions in C# ? (Refer section 13.2)
+   Q.4 What are Pointers in C# ? (Refer section 13.1)
+   Q.5 What is the purpose of Reflection ? (Refer section 13.3)
+   Q.6 Discuss exception handling in detail. (Refer section 13.2) AU : Dec.-17, May-16
+   Q.7 How will you implement security in a site ? Show the different steps. (Refer section 13.3.1) AU : Dec.-17, May-16
+   Q.8 Write a C# program to demonstrate IndexOutOfRange Exception. AU : May-18, Marks 6

Ans. :

```
/*
 * C# Program to Demonstrate IndexOutOfRange Exception
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace exceptionsdemo
{
    class arrayoutofindex
    {
        public void calculatedifference()
        {
            int diff=0;
            int [] number= new int[5] {1,2,3,4,5};
            try
            {
                for (int init =1; init <=5; init++)
                {

```