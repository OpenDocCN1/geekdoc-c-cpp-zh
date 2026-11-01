
## Beginner’s Guide to... Programming the

![](img/a9229e7b0ddd9608f171b22b52514f39_0_0.png)

## PIC24/dsPIC33

Thomas Kibalo

> "He who refuses to embrace a unique opportunity loses the prize as surely as if he tried and failed"
> - William James

- Running the experiment... 89
- 16 bit Micro Experimenter (optional)... 92
- **Chapter 5 – Using an LCD Display with the Microstick II**... 95
  - Hardware description... 95
  - Software Library Description... 98
  - Experiment #1 – LCDDEMO... 101
  - Running LCDDEMO... 102
  - Experiment #2 – A Simple Voltmeter... 103
  - Running the voltmeter... 105
  - 16 Bit Micro Experimenter (optional)... 106
- **Chapter 6 – Using Timers and Timer Interrupts**... 109
  - The 16 bit Timer peripheral... 109
  - Hardware description... 111
  - Timer 1 Experiment – non-Interrupt... 113
  - Timer 1 - 16 bit execution... 115
  - Timer 1 - 16 bit Experiment using Interrupt... 116
  - The 32 bit Timer Using Timer Peripheral Pairs... 118
  - Timer3/4 32 Bit Operation – Non Interrupt... 119
  - Timer3/4 32 Bit Operation Interrupt... 121
  - 16 bit Micro Experimenter (optional)... 122
- **Chapter 7 – Serial Communications**... 125
  - Serial Communications Overview... 125
  - RS-232 and RS-485 Industry Standard Serial Communications... 127
  - American Standard Code for Information Interchange (ASCII)... 128
  - USB (Universal serial Bus)... 130
  - Serial Communications Review... 131
  - The PIC24H Peripheral Programming System (PPS)... 132
  - Initializing PPS... 134
  - Experiment 1 "Implementing a Serial interface with a PC"... 136
  - Software Configuration... 137
  - Hardware Configuration... 138
  - Executing the code... 140
  - Using USB instead of RS-232... 143
  - 16 bit Micro Experimenter (optional)... 145

An embedded design cycle starts first with designing and entering source code for the target application, and then working through any source code syntax errors associated with the target code's software language to achieve an executable form of this source code. This executable form of source code is designated as object code. The next critical step, in this cycle, is to program the object code into your microcontroller prototype in order to test and validate the original code design. At this point in the cycle an external tool device is required to program the microcontroller. This tool type, like the Microchip's Microstick II, allows "In-Circuit Programming" to enable you to program the microcontroller while it is in the prototype without having to remove it.

Ok, let's assume we are far enough along in the embedded design cycle where we now have executable object code programmed in the prototype. We now begin the next step of testing our source code design. Nine times out of ten all code as initially designed will have latent logic errors that need to be identified and fixed. As designers, all of us are "only too human", and, as such, are fallible in making mistakes. The mistakes at this point in the cycle are not syntax source code errors but are logic errors that are implicit in the original source code design. These logic errors are always, in the end, ultimately linked with any assumptions you as the designer may have made about the application or the microcontroller hardware. This is where debug comes "to the rescue".

In debug we need to test and exercise those original assumptions and discover if they are correct or not. The IDE helps us here, and with the support of an external debugger, allows operational test and control of the microcontroller "in-circuit" with the ability to view its operation in an investigative way. For example, you should be able, in real time, to examine memory, single step the microcontroller operations, or halt operation at a designated point in the code. As you apply these tools, with your own careful thinking, you begin to uncover the latent errors or "bugs" in the design.

Now the real chore becomes reworking the source code, making changes to the source code to fix the problem, and then verifying the fix by running through the entire cycle once again. The process, in fact, relies on multiple iterations through the embedded design cycle. For each of these iterations you will continue to discover the bugs, and fix those, eventually converging on a baseline solution that is hopefully bug free. There are some experts that believe that all designs reach product maturity with some measure of latent bugs still present (I tend to believe them). The amount of time you spend in iteration is dependent on a number of factors, like the total complexity of the design, your complete understanding of the application that you designed to, your skills with the tools, your knowledge of the microcontroller, and finally, and most importantly, the number of assumptions you have made on all the above. A lot of these factors will definitely tend to diminish with experience, as both your skills with the tools and knowledge of the technology grows.

## Chapter 1 – Getting Started

In this chapter we will guide you through the installation process for Microchip MPLAB, the Microchip 'C' compiler, and the Microstick II programmer/debugger. We will test this total install using the demo project "FLASH_LED" to ensure that all elements of the install are correct and complete. We will then cover some of the important hardware elements of our tool suite, starting with an overview of Microchip's 16 bit Microcontroller family, and then covering in more detail the PIC24H, and then finally discussing the Microstick II and its operation. This chapter will serve as the foundation for all other chapters, and will leave us with the necessary development tool suite, and hardware overviews, for all subsequent chapter discussions and experiments.

Special Note: The hardware setup and projects described in this book are written for the PIC24H. They are easily configurable with a few simple steps for both the PIC24F and the dsPIC33. Details are at the end of this chapter.

### Introducing Microchip MPLAB IDE

To reiterate at this point, the Microchip MPLAB IDE is a Windows based program that runs on a PC and is used to develop applications for Microchip microcontrollers. As an IDE, it provides a single integrated "environment" to develop and test code, as part of the embedded design cycle required for all microcontrollers. The environment assists the designer in progressing through the "embedded design cycle" without the distraction of switching among an array of distinct and different tools, and allows for the designer to concentrate on completing the application without the interruption of using these separate tools and their associated specific different modes of operation.

Again, MPLAB IDE, as a framework, functions as a "wrapper" in that it coordinates all the tools from a single graphical user interface. For instance, once code is written, it must be converted to executable instruction set (object code) and then downloaded and programmed into a microcontroller to determine how well it works. During this process multiple tools are needed: an editor to write the code, a project manager to organize files and settings, a compiler to convert the source code to object code and then a hardware programmer/debugger to test the object code in operation with the microcontroller. MPLAB along with the Microstick II programmer/debugger meets all these requirements, and will serve in this book as our basic development environment.

The basic components and features of MPLAB are shown in the Figure 1-1. In the chapters to follow we will continue to discuss and illustrate the detailed use of this integrated tool set as a part of each chapter's "hands-on" experiments.

### MPLAB® Integrated Development Environment

- GUI Based
- Integrated Project Manager
  - Organizes and maintains project file space
  - Retains the workspace layout
  - Provides quick view of all functions/symbols
  - Automatic build operations (single button)
- Syntactic Source code editor
  - Color syntax-assisted assembly and C code entry/review
- Language tools
  - MPASM assembler, MPLINK linker, MPLIB library tool
  - C30 C compiler (free student version)
  - Extensive Library support (Audio, Wireless, graphics, Ethernet, USB)
- Programming and Debug capability
  - Fully compatible with Microstick
- Debug
  - Simulation (MPLAB SIM software simulator) or in-circuit with Microstick debug
  - Extensive tool sets
  - Breakpoint, single step and animate operations
  - Stopwatch, Logic Analyzer, Variable Watch, DCM, memory gauges

![](img/a9229e7b0ddd9608f171b22b52514f39_15_0.png)
