# 1.9.3.5.1 STACK

The stack is a data structure that occupies an area in memory. It has finite size and supports several operations. Its structure is similar to an array except that, unlike an array, data can be entered or removed on only one location called the top. The top of the stack is equivalent to the 0th index in an array. When a new piece of data is entered, everything below is pushed down like a stack of trays in a cafeteria or like the last card in a discard pile in a card game. When a piece of data is removed, all data below move up, again, like a stack of plates or the new top card.

+   top

+   push, pop

Figure 1.39 illustrates a model for the operations for several pieces of data. Data entry is called a push and data removal is called a pop. In reality, such a model is impractical because of the time burden in moving every piece of data each time a new entry is made. A more practical implementation adds or removes data at the open end of the structure. The memory address reflecting the current top of the stack is remembered and modified after each addition or removal. Such an address is called a stack pointer.

+   stack pointer

![](bbox=[0.28, 0.35, 0.6, 0.45])

Figure 1.39 Stack Operations

Figure 1.40 presents a modified version of Figure 1.39 and illustrates how the stack pointer is properly managed.

![](bbox=[0.28, 0.53, 0.65, 0.65])

Figure 1.40 Managing the Stack Pointer

# 1.9.3.5.2 PUSH

The push operation puts something onto the top of the stack where it is held for later use. Mechanically, the push operation increments the address that is held by the stack pointer to refer to the next empty spot (the new top of the stack) and then writes the data to be stored into the address in memory designated by that address. As we see in Figure 1.40, for ease of implementation, the address contained in the stack pointer is typically incremented from a lower memory address to higher memory address.

# 1.9.3.5.3 POP

The pop operation takes something off the top of the stack by first retrieving the value in the memory location designated by the stack pointer and then decrementing the address that is