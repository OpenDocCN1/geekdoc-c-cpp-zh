After the AVRASM2 program runs with the options passed to it as described, its output is displayed in the Output window of Microchip Studio below the line used to invoke it. The output from AVRASM2 from the test_asm project built for the ATtiny85 is as follows, with two of the file paths shortened so that each uses one line of the page.

```
AVRASM: AVR macro assembler 2.2.8 (build 80 Jan 14 2020 18:27:59)
Copyright (C) 1995-2020 ATMEL Corporation
[builtin(2): Including file 'C:/Program Files\ ... \avrasm\inc\tn85def.inc'
[builtin(2): Including file 'C:/Program Files\ ... \avrasm\inc\tn85def.inc'
"ATtiny85" memory usage summary [bytes]:
Segment Begin End Code Data Used Size Use%
[ .cseg] 0x000000 0x0000e0 14 0 14 8192 0.2%
[ .dseg] 0x000060 0x000060 0 0 0 512 0.0%
[ .eseg] 0x000060 0x000060 0 0 0 512 0.0%
Assembly complete, 0 errors. 0 warnings
```

As can be seen in the above listing, AVRASM2 outputs the memory used by the program and the number of errors and warnings generated. This same information is found at the bottom of the list file, which is test_asm.lss for this project. The list file can be opened in Microchip Studio by expanding the Output Files item in the Solution Explorer pane, where double-clicking the file test_asm.lss opens it. The Output Files item can only be expanded if the project was built without errors.

# 12.1.1.2 AVRASM2 on the Command Line

When Microchip Studio is installed on a computer, an item called Microchip Studio Command Prompt is also installed. This item can be found by opening the main Windows menu by clicking the Windows “Start” icon at the bottom left of the desktop. Scroll down this menu to find the Microchip Studio folder, which must be expanded by clicking it. After expanding the menu folder, click the Microchip Studio Command Prompt item. This opens a command prompt window that has the Microchip Studio tools in its path. AVRASM2 can be invoked from this command prompt window. Entering just the name of AVRASM2 at the command prompt, as shown below, prints the version, build and copyright information.

```
avrasm2
```

Invoking AVRASM2 and passing it the -h option or switch, as shown below, causes it to print out all of the command line options.

```
avrasm2 -h
```