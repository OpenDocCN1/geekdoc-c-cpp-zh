
The activation record for sub is shown in Figure 10.4.

Activating a subprogram requires the dynamic creation of an instance of the activation record for the subprogram. As stated earlier, the format of the activation record is fixed at compile time, although its size may depend on the call in some languages. Because the call and return semantics specify that the subprogram last called is the first to complete, it is reasonable to create instances of these activation records on a stack. This stack is part of the run-time system and therefore is called the run-time stack, although we will usually just refer to it as the stack. Every subprogram activation, whether recursive or nonrecursive, creates a new instance of an activation record on the stack. This provides the required separate copies of the parameters, local variables, and return address.

One more thing is required to control the execution of a subprogram—the EP. Initially, the EP points at the base, or first address of the activation record instance of the main program. The run-time system must ensure that it always points at the base of the activation record instance of the currently executing program unit. When a subprogram is called, the current EP is saved in the new activation record instance as the dynamic link. The EP is then set to point at the base of the new activation record instance. Upon return from the subprogram, the stack top is set to the value of the current EP minus one and the EP is set to the dynamic link from the activation record instance of the subprogram that has completed its execution. Resetting the stack top effectively removes the top activation record instance.

## Figure 10.4
The activation record for function sub

|  |  |
|---|---|
| Local | sum |
| Local | list [4] |
| Local | list [3] |
| Local | list [2] |
| Local | list [1] |
| Local | list [0] |
| Parameter | part |
| Parameter | total |
| Dynamic link |  |
| Return address |  |

The EP is used as the base of the offset addressing of the data contents of the activation record instance—parameters and local variables.

Note that the EP currently being used is not stored in the run-time stack. Only saved versions are stored in the activation record instances as the dynamic links.

We have now discussed several new actions in the linkage process. The lists given in Section 10.2 must be revised to take these into account. Using the activation record form given in this section, the new actions are as follows:

The caller actions are as follows:
- 1. Create an activation record instance.
- 2. Save the execution status of the current program unit.
- 3. Compute and pass the parameters.
- 4. Pass the return address to the called.
- 5. Transfer control to the called.

The prologue actions of the called are as follows:
- 1. Save the old EP in the stack as the dynamic link and create the new value.
- 2. Allocate local variables.

The epilogue actions of the called are as follows:
- 1. If there are pass-by-value-result or out-mode parameters, the current values of those parameters are moved to the corresponding actual parameters.
- 2. If the subprogram is a function, the functional value is moved to a place accessible to the caller.
- 3. Restore the stack pointer by setting it to the value of the current EP minus one and set the EP to the old dynamic link.
- 4. Restore the execution status of the caller.
- 5. Transfer control back to the caller.

Recall from Chapter 9, that a subprogram is active from the time it is called until the time that execution is completed. At the time it becomes inactive, its local scope ceases to exist and its referencing environment is no longer meaningful. Therefore, at that time, its activation record instance can be destroyed.

Parameters are not always transferred in the stack. In many compilers for RISC machines, parameters are passed in registers. This is because RISC machines normally have many more registers than CISC machines. In the remainder of this chapter, however, we assume that parameters are passed in

## 10.3.2 An Example Without Recursion

Consider the following skeletal C program:

```
void fun1(float r) {
    int s, t;
    ...          <---------- 1
    fun2(s);
    ...
}
```

```
void fun2(int x) {
    int y;
    ...          <---------- 2
    fun3(y);
    ...
}
```

```
void fun3(int q) {
    ...          <---------- 3
}
```

```
void main() {
    float p;
    ...
    fun1(p);
    ...
}
```

The sequence of function calls in this program is

```
main calls fun1
fun1 calls fun2
fun2 calls fun3
```

The stack contents for the points labeled 1, 2, and 3 are shown in Figure 10.5.

At point 1, only the activation record instances for function main and function fun1 are on the stack. When fun1 calls fun2, an instance of fun2's activation record is created on the stack. When fun2 calls fun3, an instance of fun3's activation record is created on the stack. When fun3's execution ends, the instance of its activation record is removed from the stack, and the EP is used to reset the stack top pointer. Similar processes take place when functions fun2 and fun1 terminate. After the return from the call to fun1 from main, the stack has only the instance of the activation record of main. Note that some implementations do not actually use an activation record instance on the stack

## Figure 10.5
Stack contents for three points in a program

ARI = activation record instance

at Point 1

at Point 2

at Point 3

for main functions, such as the one shown in the figure. However, it can be done this way, and it simplifies both the implementation and our discussion. In this example and in all others in this chapter, we assume that the stack grows from lower addresses to higher addresses, although in a particular implementation, the stack may grow in the opposite direction.

The collection of dynamic links present in the stack at a given time is called the dynamic chain, or call chain. It represents the dynamic history of how execution got to its current position, which is always in the subprogram code whose activation record instance is on top of the stack. References to local variables can be represented in the code as offsets from the beginning of the activation record of the local scope, whose address is stored in the EP. Such an offset is called a local_offset.

The local_offset of a variable in an activation record can be determined at compile time, using the order, types, and sizes of variables declared in the subprogram associated with the activation record. To simplify the discussion, we assume that all variables take one position in the activation record. The first local variable declared in a subprogram would be allocated in the activation record two positions plus the number of parameters from the bottom (the first two positions are for the return address and the dynamic link). The second local variable declared would be one position nearer the stack top and so forth. For example, consider the preceding example program. In fun1, the local_offset of s is 3; for t it is 4. Likewise, in fun2, the local_offset of y is 3. To get the address of any local variable, the local_offset of the variable is added to the EP.

## 10.3.3 Recursion

Consider the following example C program, which uses recursion to compute the factorial function:

```
int factorial(int n) {
    <---------- 1
    if (n <= 1)
        return 1;
    else return (n * factorial(n - 1));
    <---------- 2
}
void main() {
    int value;
    value = factorial(3);
    <---------- 3
}
```

The activation record format for the function factorial is shown in Figure 10.6. Notice that it has an additional entry for the return value of the function.

Figure 10.7 shows the contents of the stack for the three times execution reaches position 1 in the function factorial. Each shows one more activation of the function, with its functional value undefined. The first activation record instance has the return address to the calling function, main. The others have a return address to the function itself; these are for the recursive calls.

Figure 10.8 shows the stack contents for the three times that execution reaches position 2 in the function factorial. Position 2 is meant to be the time after the return is executed but before the activation record has been removed from the stack. Recall that the code for the function multiplies the current value of the parameter n by the value returned by the recursive call to the function.

## Figure 10.6
The activation record for factorial

| Functional value |
| Parameter | n |
| Dynamic link |
| Return address |
