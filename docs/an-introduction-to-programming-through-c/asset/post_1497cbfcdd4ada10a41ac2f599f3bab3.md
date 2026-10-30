
The exact format in which real numbers are represented on modern computer hardware and in C++ is the IEEE Floating Point Standard. It is much more complicated, but has more features, some of which we will discuss later.

## 2.4 Organization of a computer

We can think of a computer as consisting of the following main parts. An actual computer will contain more parts, but all are not of interest to us in this high level sketch.

- 1. Main memory. In this we store the numbers on which we are performing our calculations. As we will see later, the memory will also hold the program.
- 2. Arithmetic unit. This is capable of performing arithmetic. We supply to it the operands, tell it what operation we want performed, and it does so. We can then extract the result and store it back in memory.
- 3. Input-output devices. There can be many, but we consider the keyboard, the display, which is often referred to as the monitor or the screen, and the disk.
- 4. Control Unit. This controls the other units, as the name implies.
- 5. Network. This is useful for moving data between the parts.

It is customary to use the term Central Processing Unit to denote the control unit together with the arithmetic unit.

You may think of each part as consisting of a box with circuitry inside. Each part has ports (sets of wires) on which data can come out from the part or go into the part. It is possible to take the data out of one part and send it to another part through the network. How exactly the data flows is determined by the control unit. This organization is sketched in Figure 2.3. The control unit has connections to every other unit, we have not shown them in the picture to avoid clutter.

## 2.5 Main memory

The memory of a modern computer may contain a huge number of basic memory elements, say 2^35. These are usually capacitors as discussed earlier. Each basic memory element is capable of storing 1 bit. The number of bits that can be stored is defined to be the capacity, or the size, of the memory. More commonly, the memory size is measured in bytes, where a byte is simply 8 bits. Thus a memory with 2^35 capacitors has size 2^35 bits or 2^32 bytes, or 4 Gigabytes.

### 2.5.1 Addresses

![](img/c7233aedab7e4c7cad32a7615b6a4783_39_0.png)

# Figure 2.3: Computer Organization (sketch)

labels from 1 to N, on computers it is more customary to start with 0. The address of a byte is useful for identifying it from among all the bytes in the memory. Note that addresses are unsigned integers. Thus they can be represented using their binary representation.

The phrase "byte x" is commonly used to mean the byte whose address is x. The phrase "word x" is also used, this simply means the word starting at byte x, i.e. the set of bytes x, x + 1, x + 2, x + 3. Similarly for half-words and double words.

The phrase "location x" is also used; usually it means the word starting at address x. However, it may mean byte x or double word x based on the context.

### 2.5.2 Ports and operations

A memory communicates with the rest of the world using 2 sets of wires or ports. The first is the address port, and the second the data port. There are also two additional wires connecting to the memory: we will call the first the read control port and the second the write control port. Using these we can access the contents of the memory as follows. In what follows we use the phrase "place a quantity" to mean "place the representation of that quantity".

- 1. Storing data into byte x: For this it is necessary to place the address x on the address port, and the data that you want stored, say the number y, on the data port. Then you place the number 1 on the write control port. This signals the memory to store the data on the data port into the byte whose address is present on the address port.

Thus the number y will be stored in byte x. Byte x will continue to hold the number y until another write operation is performed on byte x.

- 2. Reading data from byte x: For this, you place the address x, on the address port. Then you place a 1 on the read control port. The 1 on the read control port signals the memory to sense the data stored in byte x of the memory and place it on the data port. Once data appears on the data port, it can be moved from there to where it is needed.

What we described above is a byte-oriented memory. More common are word-oriented memories. In these, when we supply an address, the word starting at the given address is sent back or written to. In byte-oriented memories, the data port will consist of 8 wires, because 8 bits need to be communicated. In word-oriented memories, the data port will likewise have to have 32 wires. Similarly for half-words and double word oriented memories.

How many wires do we need in the address port? Let us take our 2^32 byte memory as an example. In this memory, the addresses range from 0 to 2^32 − 1. Thus the largest address consists of 32 consecutive 1s. Hence the address port will have to have 32 wires, in order that we may specify any possible address. In general, if the memory has N bytes, then we will need to have log2 N wires in the address port.

## 2.6 The arithmetic unit

The arithmetic unit has circuits using which it is possible to perform basic arithmetic operations, i.e. addition, subtraction, multiplication, division, for numbers in all formats described earlier, unsigned and signed integers, and floating. It receives the operands through two ports named Input1 and Input2 and the result of the operation is placed on the port named Output, see Figure 2.3. What operation is to be performed depends upon the value supplied on the Control port. The arithmetic unit can also convert numbers from one representation to another, e.g. given a number represented as an integer on one of the inputs, its representation in the floating format (exponent and significand) can be produced on the output port.

You may think that the arithmetic unit must consist of many very complicated circuits. That is indeed true. However, for the purpose of programming, we don’t need to know how the circuits are to be designed, it is sufficient to know what they can do.

## 2.7 Input-Output Devices

The input-output devices are considered to be peripherals, and the rest of the computer the “main computer”.

### 2.7.1 Keyboard

The simplest input device is a keyboard. A code number is assigned to each key on the keyboard. When a key is pressed, the corresponding code number is sent to the main

However, the fundamental ideas should be noted: (a) communication between the main computer and the peripheral device happens by sending numbers, (2) information is stored as bits, by designating some physical property to determine whether a 0 or a 1 is stored (3) if several bits are stored, there will be a notion of *address* using which we can refer to some selected bit or group of bits.

## 2.8 The Control Unit

As the name implies, the Control Unit controls the other parts of a computer. The control unit contains complex circuitry. But it is possible to understand its function at a high level.

When you want to solve a problem, you would like the computer to perform a certain sequence of operations, depending upon the algorithm you have decided for the problem. To take a simple example, suppose you want to compute the cube of a number. Then you would like the number to be read from the keyboard and put into some location in memory, say the word at address 100. After that you would like the arithmetic unit to multiply the number at the location by itself, two times and then put the result at some other location, say location 104. Finally, you would like the number at location 104 to be displayed on the screen. If you want to solve some other problem, then a different sequence of operations would have to be performed.

The control unit can get the other parts of the computer to perform whatever action you may desire, including the actions noted above. However, you must somehow tell the control unit what you want. How do you do this?

Here is the outline of the answer: you store the sequence of actions you want performed in the memory of the computer, and then ask the control unit to perform those actions, in the order you have stored them. Many details need to be explained: (a) how do we store action sequences in memory, (b) can we design circuits using which the control unit can “understand” what is stored in memory and perform the required action. The answer to part (b) is Yes, the control unit indeed contains the required circuits, but any explanation of these circuits is outside the scope of this book.

A high level answer to part (a) is as follows. It follows the basic idea that on a computer, everything is represented using numbers, including actions that you want the computer to perform! The computer designer provides you with a numerical coding system called *machine language* using which you can tell the control unit what you want. As an example, the computer designer may decide that (a) the sequence of numbers of the form 53, *x* (for any *x*) means the control unit should perform the actions needed to read a real number from the keyboard and put it into the memory location *x*, (b) sequences of the form 57, *x, y, z* mean the control unit should perform the actions needed to multiply the real numbers in locations *x, y* and store the result in location *z*, (c) sequences of the form 63, *x* mean the control unit should perform the actions needed to display the real number in location *x* on the screen, and (d) the sequence consisting of just the number 99 means the control unit should shut down the computer. Each such sequence of numbers is called a machine instruction, and a sequence of machine instructions is called a machine language program. Thus, the sequence of numbers 53, 100, 57, 100, 100, 104, 57, 100, 104, 104, 63, 104, 99 would represent a machine language program consisting of the instructions:
