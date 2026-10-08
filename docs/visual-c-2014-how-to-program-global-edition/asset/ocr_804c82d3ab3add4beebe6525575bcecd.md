# Special Section: Building Your Own Computer 403

After each line is displayed, test for whether either animal has reached or passed 70. If so, display the winner and terminate the simulation. If the tortoise wins, display TORTOISE W!!! YAY!!! If the hare wins, display Hare wins.. Yuch. If both animals are on the same tick of the clock, you may want to favor the tortoise ('underdog'), or you may want to display It's a tie. If neither wins, perform the loop again to simulate the next tick of clock. When you're ready to run your app, assemble a crowd of fans to watch the race. You'll be amazed at how involved your audience gets!

8.29 (Card Shuffling and Modifying) 8.12 to define a five-card poker hand. Then modify class DeckOfCards of 8.11 to include methods that determine whether a hand contains

+   - a pair
- two pairs
- three of a kind (e.g., three jacks)
- four of a kind (e.g., four aces)
- a flush (i.c., all cards of the same suit)
- a straight (i.c., five cards of consecutive face values)
- a full house (i.c., two cards of one value and three cards of another value)

8.30 (Merging Arrays) Write a program to merge two arrays of the same size, sorted in ascending order. Test the program with relevant values

# Special Section: Building Your Own Computer

In the next problems, we take a temporary diversion from the world of high-level language programming to "peer open" a computer and look at its internal structure. We introduce machine-language programming and write several machine-language programs. To make this a valuable experience, we will build a computer (through the technique of software-based simulation) on which you can execute your machine-language programs.

8.31 (Machine-Language Programming) Let's create a computer like the Simple. As its name implies, it's simple, but powerful. The Simple runs programs written in the only language it understands: Simple Machine Language, or SML for short.

The Simple contains an accumulator--a special register where information is put before the Simple uses it in calculations or evaluations in various ways. All the information in the Simple is handled in words. A word is a signed-digit decimal number, such as +3364, -1293, +0000 and -0001. The Simple is equipped with a 100-word memory, and words are referenced by their location numbers 00, 01, ..., 99.

Before running an SML program, we must load, or place, the code into the memory. The first instruction (or statement) of every SML program is always placed in location 00. The Simple will start executing that instruction.

Each instruction in SML occupies one word of the Simple's memory (hence instructions are four-digit numbers). We assume that the sign of an SML instruction is always plus, but the sign of a data may be plus or minus. In the Simple's memory contains an instruction, a value used by a program or an (hence undefined) area of memory. The first two digits of each SML instruction are the operation code specifying the operation to be performed. SML operations are counted in Fig. 8.31.

The last two digits of each instruction are the address--the address of the memory location containing the operation applies. Let's consider several simple programs. The first SML program, +1007 reads the first number from the keyboard, and then displays them. Then puts it into location 07 (which was initialized to 0). Then instruction +1008 reads the next number into location 08. The load instruction, +2007, puts the first number into the accumulator, and the add instruction, +3008, adds the second number to the number in the accumulator. All SML arith-