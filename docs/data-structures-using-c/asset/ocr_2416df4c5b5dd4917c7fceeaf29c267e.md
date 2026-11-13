![](bbox=[0.313, 0.112, 0.783, 0.68])

# 3.10 REVERSING A STRING WITH A STACK

Suppose a sequence of elements is presented and it is desired to reverse the sequence. Various methods could be used for this, and in the beginning, the programmer will usually suggest a solution using an array. A conceptually simple solution, however, is based on using a stack. The LIFO property of the stack access guarantees the reversal.

Suppose the sequence ABCDEF is to be reversed. With a stack, one simply scans the sequence, pushing each element onto the stack as it is encountered, until the end of the sequence is reached. The stack is then popped repeatedly, with each popped element sent to the output, until the stack is empty. Table 3.13 illustrates this algorithm: