ERASE2 The alternate erase character (backspace). This character is treated exactly like the erase character (ERASE).

INTR The interrupt character. This character is recognized on input if the ISIG flag is set and generates the SIGINT signal that is sent to all processes in the foreground process group (refer to Figure 9.7). This character is discarded when processed (i.e., it is not passed to the process).

KILL The kill character. (The name “kill” is overused; recall the kill function used to send a signal to a process. This character should be called the line-erase character; it has nothing to do with signals.) It is recognized on input in canonical mode (ICANON). It erases the entire line and is discarded when processed (i.e., it is not passed to the process).

LNEXT The literal-next character. This character is recognized on input in extended mode (IEXTEN) and causes any special meaning of the next character to be ignored. This works for all special characters listed in this section. We can use this character to type any character to a program. The LNEXT character is discarded when processed, but the next character entered is passed to the process.

NL The newline character, also called the line delimiter. We cannot change this character. It is recognized on input in canonical mode (ICANON). This character is returned to the reading process.

QUIT The quit character. This character is recognized on input if the ISIG flag is set. The quit character generates the SIGQUIT signal, which is sent to all processes in the foreground process group (refer to Figure 9.7). This character is discarded when processed (i.e., it is not passed to the process).

Recall from Figure 10.1 that the difference between INTR and QUIT is that the QUIT character not only terminates the process by default, but also generates a core file.

REPRINT The reprint character. This character is recognized on input in extended, canonical mode (both IEXTEN and ICANON flags set) and causes all unread input to be output (reechoed). This character is discarded when processed (i.e., it is not passed to the process).

START The start character. This character is recognized on input if the IXON flag is set and is automatically generated as output if the IXOFF flag is set. A received START character with IXON set causes stopped output (from a previously entered STOP character) to restart. In this case, the START character is discarded when processed (i.e., it is not passed to the process).

When IXOFF is set, the terminal driver automatically generates a START character to resume input that it had previously stopped, when the new input will not overflow the input buffer.