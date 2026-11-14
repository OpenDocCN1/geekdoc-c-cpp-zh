any arbitrary event. Some are designated to signal specific events; one for each different timer in the system, one for detecting a bad or illegal op-code, or one to signify that an analog-to-digital conversion is complete are serious examples.

We also often find that interrupts are assigned different priorities. The processor manufacturer may specify that a timer interrupt has a higher priority than the conversion complete signal from the A/D or the bad op-code interrupt higher than both. Such a priority scheme is used to handle the cases of several interrupts occurring at the same time or an urgent condition occurring while we are working on a less critical one. Interrupts are generally numbered, in order of decreasing priority, from 0 to n–1, if we have n interrupts.

# 7.7.3 The Interrupt Service Routine – ISR

interrupt service routine (ISR) When an interrupt occurs, it is necessary to do something, and to be able to do something, one must know what one is supposed to do. In a software program, one knows what needs to be done, and that is accomplished by executing a series of instructions. With a function, the task to be accomplished comprises the body of the function. For the interrupt, that body of code is called the ISR.

The structure of an ISR is no different from the functions with which we have been dealing. With no other contextual information, one could not tell them apart. The template for an ISR is given in Figure 7.45.

```
void ISRName(void)
{
 body
}
```

Figure 7.45 A Template for an Interrupt Service Routine (ISR)

Observe that the return type is specified as void and that the function’s signature is similarly specified as void.

One must write an ISR for each interrupt that will be used in a system; the reason will become clear very shortly.

> Coding Style
> 
> When we write an ISR, our goal should be to make that routine as short and simple as possible. While we are in the routine, we are spending time away from the main line code, which is typically our primary focus. An ISR that exceeds 15–20 lines of C code is probably too long.

# 7.7.4 The Interrupt Vector Table

When one writes and uses a function, one specifies the prototype and defines the function body. To invoke the function, one enters the name of the function, with the appropriate arguments, as a line of code in the program. When the program flow reaches the line of code containing the call, a context switch to the code comprising the function body is made and the code is executed, as discussed earlier.

The interrupt presents a more interesting challenge. Since the interrupt is asynchronous to the normal flow in the program, there is no place to put the call. There must be another scheme; this is where the interrupt vector table comes in.