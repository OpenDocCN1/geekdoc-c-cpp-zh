
### 7.5 *(Write C++ Statements)*

For each of the following, write a single statement that performs the specified task. Assume that long variables value1 and value2 have been declared, and value1 has been initialized to 200000.

- a) Declare the variable longPtr as a pointer to an object of type long.
- b) Assign the address of variable value1 to pointer variable longPtr.
- c) Display the value of the object pointed to by longPtr.
- d) Assign the value of the object pointed to by longPtr to variable value2.
- e) Display the value of value2.
- f) Display the address of value1.
- g) Display the address stored in longPtr. Is it displayed the same as value1’s?

### 7.6 *(Find the Code Errors)*

Find the error in each of the following segments. If the error can be corrected, explain how.

- a)

    int* number;
    cout << number << '\n';

- b)

    double* realPtr{nullptr};
    long* integerPtr{nullptr};
    integerPtr = realPtr;

- c)

    char s[]{"this is a character array"};
    for (; *s != '\0'; ++s) {
        std::cout << *s << ' ';
    }

- d)

    double x{19.34};
    double xPtr{&x};
    cout << xPtr << '\n';

### 7.7 *(Cubing the Elements of a span)*

Use the techniques demonstrated in Fig. 7.12 to create a cubeElements function that cubes the elements of its argument. Enable the function to receive as its argument a built-in array, std::array or std::vector. Test your function using values1, values2 and values3:

```
int values1[]{1, 2, 3, 4, 5};
std::array values2{6, 7, 8, 9, 10};
std::vector values3{11, 12, 13, 14, 15};
```

Use Fig. 7.12’s dispSpan function to display values1, values2 and values3 before and after cubing each.

### 7.8 *(Simulation: The Tortoise and the Hare)*

Let’s re-create the classic race of the tortoise and the hare (https://en.wikipedia.org/wiki/The_Tortoise_and_the_Hare). You’ll use random-number generation to develop a simulation of this memorable event.

Our contenders begin the race at “square 1” of 70 squares. Each square represents a position along the racecourse, and the finish line is at square 70. The first contender to reach or pass square 70 is rewarded with a pail of fresh carrots and lettuce. The course weaves its way up the side of a slippery mountain, so occasionally, the contenders lose ground.

There is a clock that ticks once per second. With each clock tick, your program should use functions moveTortoise and moveHare to adjust the animals’ positions according to Fig. 7.15’s rules. These functions should use pointer-based pass-by-reference to modify the position of the tortoise and the hare.

| Animal | Move type | Percentage of the time | Actual move |
|---|---|---|---|
| Tortoise | Fast plod | 50% | 3 squares to the right |
|  | Slip | 20% | 6 squares to the left |
|  | Slow plod | 30% | 1 square to the right |
| Hare | Sleep | 20% | No move at all |
|  | Big hop | 20% | 9 squares to the right |
|  | Big slip | 10% | 12 squares to the left |
|  | Small hop | 30% | 1 square to the right |
|  | Small slip | 20% | 2 squares to the left |

**Fig. 7.15** | Rules for moving the tortoise and the hare.

Use variables to keep track of the positions of the animals (i.e., position numbers are 1–70). Start each animal at position 1 (i.e., the “starting gate”). If an animal slips left before square 1, move the animal back to square 1.

Generate the percentages in Fig. 7.15 by producing a random integer *i* in the range 1 ≤ *i* ≤ 10. For the tortoise, perform a “fast plod” when 1 ≤ *i* ≤ 5, a “slip” when 6 ≤ *i* ≤ 7 or a “slow plod” when 8 ≤ *i* ≤ 10. Use a similar technique to move the hare.

Begin the race by displaying

```
BANG !!!!!!
AND THEY'RE OFF !!!!!!
```

For each clock tick (i.e., each iteration of a loop), display a 70-position line showing the letter T in the tortoise’s position and H in the hare’s position. When the contenders land on the same square, the tortoise bites the hare, and your program should display “OUCH!!!” beginning at that position. All positions other than the T, the H or the OUCH!!! (in case of a tie) should be blank.

After displaying each line, test whether either animal has reached or passed square 70. If so, display the winner and terminate the simulation. If the tortoise wins, display “TORTOISE WINS!!! YAY!!!” If the hare wins, display “Hare wins. Yuch.” If both animals win on the same clock tick, you may want to favor the tortoise (the “underdog”), or you may want to display “It’s a tie”. If neither animal wins, perform the loop again to simulate the next clock tick.

## Special Section—Building Your Own Computer as a Virtual Machine

The next several exercises temporarily diverge from the world of high-level language programming. We “peel open” a fake simple computer and look at its internal structure. We introduce simple machine-language programming for this computer and write several machine-language programs. To make this an especially valuable experience, we then build a software-based *simulation* of this computer on which you actually can execute your machine-language programs! Such a simulated computer is often called a virtual machine.

### 7.9 (Machine-Language Programming)

Let’s create a computer we’ll call the Simpletron. As its name implies, it’s a simple machine, but as we’ll soon see, it’s powerful. The Simpletron runs programs written in the only language it directly understands—Simpletron Machine Language or SML for short.

The Simpletron contains an accumulator—a “special register” in which information is put before the Simpletron uses that information in calculations or examines it in various ways.

All information in the Simpletron is handled in terms of words. A word is a signed four-digit decimal number, such as +3364, −1293, +0007, −0001, etc.

The Simpletron is equipped with a 100-word memory, and these words are referenced by their location numbers 00, 01, …, 99.

Before running an SML program, we must load the program into memory. The first instruction (or statement) of every SML program is always placed in location 00.

Each SML instruction occupies one word of the Simpletron’s memory, so instructions are signed four-digit decimal numbers. We assume an SML instruction’s sign is always plus, but a data word’s sign may be plus or minus. Each Simpletron memory location may contain an instruction, a data value used by a program or an unused (and hence undefined) area of memory. Each SML instruction’s first two digits are the operation code specifying the operation to perform. The SML operation codes are summarized in the following table. They should be defined in a scoped enum named OperationCodes—each constant is shown with the value you should explicitly assign to it:

| Operation code | Meaning |
|---|---|
| *Input/output operations:* | |
| `read = 10` | Read a word from the keyboard into a specific memory location. |
| `write = 11` | Write a word from a specific memory location to the screen. |
| *Load/store operations:* | |
| `load = 20` | Load a word from a specific memory location into the accumulator. |
| `store = 21` | Store a word from the accumulator into a specific memory location. |
| *Arithmetic operations:* | |
| `add = 30` | Add a word from a specific memory location to the word in the accumulator (leave the result in the accumulator). |
| `subtract = 31` | Subtract a word from a specific memory location from the word in the accumulator (leave the result in the accumulator). |
| `divide = 32` | Divide a word from a specific memory location into the word in the accumulator (leave the result in the accumulator). |
| `multiply = 33` | Multiply a word from a specific memory location by the word in the accumulator (leave the result in the accumulator). |
| *Transfer-of-control operations:* | |
| `branch = 40` | Branch to a specific memory location. |
| `branchNeg = 41` | Branch to a specific memory location if the accumulator is negative. |
| `branchZero = 42` | Branch to a specific memory location if the accumulator is zero. |
| `halt = 43` | Halt—i.e., the program has completed its task. |

An SML instruction’s last two digits are the operand—the memory location containing the word to which the operation applies.
