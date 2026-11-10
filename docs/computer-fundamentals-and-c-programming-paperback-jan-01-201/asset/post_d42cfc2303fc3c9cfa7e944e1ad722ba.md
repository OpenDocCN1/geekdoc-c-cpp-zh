
**Read Only Memory (ROM)** Primary memory that in its most basic form can be read but not written. Stores special programs (like the BIOS) or information that don’t change. Erasable and programmable sub-categories available as PROM, EPROM and EEPROM.

**real number** Same as **floating-point number**.

**real-time operating system** An operating system that provides a guaranteed response time. Used in situations where the response needs to be instantaneous (like in driverless cars and process control).

**recursion** A form of coding that uses instructions to specify themselves. Concept used in a C function that repeatedly calls itself.

**recursive function** A function that repeatedly calls itself until it encounters the terminating condition which halts further recursion. Too many recursive calls can lead to **stack overflow**.

**redirection** A feature of the shell for reassigning the standard input and standard output of a program. Using the < and > symbols, redirection can direct a data stream to a disk file or originate from it.

**register** In hardware, term refers to high-speed memory that is directly connected to the CPU. In C, term refers to the storage class of a variable, which involves these high-speed registers.

**relational expression** An expression containing a relational operator (like < or ==) which evaluates to a true or false value.

**relational operator** A binary operator that tests the relationship between two operands. Represented by symbols like >, <, ==, and !=.

**ring topology** A type of networking where all nodes are connected in a loop without using a hub. Failure of one node brings down the network.

**root** The top-most directory in a hierarchical file system which has no parent. Is indicated by the / (Linux) and \ (MSDOS) symbols. Also refers to the top-most node in a **tree** data structure.

**router** A special device that routes packets from one network to another.

**runtime** Term used to refer to a program in execution. A program that clears compilation can still fail at runtime.

**scan set** A format specifier of the **scanf** function that uses a set of characters enclosed by [ and ] for matching characters that either belong or don’t belong to the set. The format specifier `%[^\n]` represents a scan set that matches an entire line not containing the newline character.

**secondary memory** Non-volatile memory that is not directly connected to the CPU. Used for offline storage and includes the hard disk, magnetic tape, CD-ROM and DVD-ROM. See also **primary memory**.

**secure shell** A set of applications used in a network that encrypts an entire session.

**selection sort** A technique used to sort data in multiple passes by comparing each data element with the start element and swapping them depending on whether one is greater or less than the other. See also **bubble sort**.

**statement** Term used to refer to an instruction in C. Unlike a preprocessor directive, a statement ends with a semicolon.

**static function** A function that is inaccessible in other program files. The keyword **static** is used in the declaration of a static function.

**static variable** A variable that is created and initialized only when the function is first called. Its value is preserved between successive calls. The keyword **static** is used in the declaration of a static variable.

**storage class** A variable attribute that determines its scope, lifetime and initial value. A variable must belong to one of four storage classes (automatic, static, external and register).

**string** An array of characters terminated by the NUL character (`'\0'`). Characters enclosed within double quotes also evaluate to a string. `scanf` and `printf` use the `%s` format specifier to match a word and complete string, respectively.

**stringizing operator** The # operator that is used with the #define directive of the preprocessor to convert a macro argument to a string constant. Solves the problem of replacing parameters inside strings. See also **token pasting operator**.

**structure** A user-defined data type meant to store heterogeneous data in its members or fields. Each member is accessed using dot and -> pointer notation. Unlike an array, a structure passed as an argument to a function is copied inside the function.

**structured programming** A programming paradigm that advocates the use of independent reusable modules for faster development and easier maintainability. Based on the premise that any computing problem can be solved using only sequencing, decision making and repetition constructs.

**structure tag** A name that represents the data type of the structure. A structure declared without a tag doesn't allow further creation of variables of its type.

**switch (hardware)** A device that is connected to multiple devices in a network. Unlike a **hub**, a switch is intelligent and broadcasts the data it receives from one node *only* to the one the data is meant for.

**switch (software)** A token normally beginning with a /, which changes the default behavior of an MSDOS command. The **DIR /P** command has /P as its switch. Counterpart in Linux is the **option** which uses a - instead of /.

**symbolic constant** A named constant defined and undefined with the **#define** and **#undef** directives of the preprocessor. Also known as **named constant**, **defined constant** and **manifest constant**.

**syntax error** An error that occurs when a statement fails to conform to the rules of the language. The compiler doesn't create the executable if it detects a syntax error.

**system software** A category of software that manages the computer hardware and its peripherals. User programs access the hardware using system software. Includes device drivers and the operating system. See also **application software**.

**tab** A single character which simulates a contiguous set of spaces. Is generated by hitting a specific key or *[Ctrl-i]*, and forms one of the characters of **whitespace**. Useful for aligning columns.

**tail pointer** A pointer that points to the last node of a **linked list**. Facilitates list access from its end and is updated when a node is added or deleted at the end.

**TCP/IP** Expands to Transmission Control Protocol/Internet Protocol—a collection of protocols used for networking computers. Ensures reliable transmission and is used on the Internet.

**ternary operator** An operator that uses the ? and : symbols along with three expressions *exp1*, *exp2* and *exp3* as operands. The value of the compound expression is either *exp2* or *exp3* depending on the logical value of *exp1*. Often replaces simple **if-else** statements.

**text file** A file that contains printable characters organized as lines and terminated by an OS-dependent newline character. The **fopen** function needs to know whether a file is to be opened in binary or text mode. See also **binary file**.

**time sharing** Term used to refer to the allotment of a small slice of time to each program, which is taken out of operation after it has used the slice. Concept used by multi-user and multi-tasking operating systems.

**token** A contiguous sequence of non-whitespace characters.

**token pasting operator** The ## operator that is used by the preprocessor to merge the two tokens on either side of the ## to a single token. See also **stringizing operator**.

**top-down programming** A programming methodology that advocates understanding the entire system before breaking it up into its individual components. See **bottom-up programming**.

**tree** A non-linear data structure whose elements are organized as a hierarchy of nodes, where child nodes are connected to their parents using pointers. An ordered binary tree speeds up search operations by halving the search domain in each descent to the next level.

**truth table** A table that lists the output of a logic gate for all possible combinations of the input. Also used with the same meaning for bitwise operations.

**two’s complement** A widely used form of representation of a negative number, obtained by reversing the bits of its positive counterpart (one’s complement) and adding 1 to it. Uses a single zero.

**unary operator** An operator that has a single operand. Includes the ++, --, ! and ~ operators.

**union** A structure-like data type where multiple members share the same memory region. The member that is updated last is also the one that is currently active, but its value can also be read back using another member.

**Universal Serial Bus (USB)** A port used universally to connect devices like mouse, printer, scanner and smartphone. Has both power and data lines.

**unresolved reference** An entry made to a table by the compiler when it encounters a function. The **linker** uses this entry to extract the code for the function from a library.
