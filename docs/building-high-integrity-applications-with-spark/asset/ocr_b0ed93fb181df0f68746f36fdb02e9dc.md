question as a result of rigorous testing, code review, or other reasons. Having program units with failing proofs is unsightly. It can also be hazardous because you become insensitive to the repeated ignorable messages from the tools. If the messages change or a new message appears that is not ignorable, you may not notice. Thus, it is highly desirable to have program units partitioned into those that prove cleanly and those that are not intended to be SPARK.

The SPARK tools do provide a means for suppressing warnings using pragma Warnings and for justifying failed proofs using pragma Annotate. See the SPARK 2014 Toolset User’s Guide (SPARK Team, 2014b) for more information. Of course, suppressing messages should be done cautiously and only after careful review or concentrated testing provides evidence of correctness.

In cases where a larger block of code contains numerous unproved verification conditions, or is even outside of SPARK, it may be more appropriate to factor the unproved code into a separate unit. This can help draw attention to the difficult code as a subject for future review. The Ada feature of private child packages is particularly useful in this context. We illustrate the technique with a simple example.

In an earlier version the SPARK tools did not have a good understanding of the effect of the bit manipulation operations.⁶ As a result, proving verification conditions related to those operations was often problematic.

Suppose one wanted to create a package implementing serveral network protocols. It would be reasonable to organize such a potentially large package as a collection of child packages working together. The top-level parent package might include declarations of interest to the entire system such as declarations of fundamental types representing the basic units of data flowing over the network. A partial specification of such a package Network follows:

```
package Network
with SPARK_Mode => On
is
    type Octet      is mod 2**8;
    type Double.Octet is mod 2**16;
end Network;
```

Children of this package might implement various network protocols such as, for example, TCP, UDP, or application protocols like SMTP. Assume that various helper subprograms that are useful when implementing multiple protocols are factored out into a child package Network.Helpers. For sake of illustration, suppose that package contained a procedure Split16 that separated a 16-bit value