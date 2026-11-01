
Ok so far, but not very exciting. The MPLAB works well --but where is the beef? We need to raise the ante. Let's close this configuration out ('click' red X button in top right hand corner of IDE) and then let's fire up a Demo project directly. Under this new scenario we should see MPLAB populated with the components of the particular demo project, displaying those functional components in MPLAB in the workspace as they were last saved.

Navigate to where you stored your demo folder, open this folder and locate the project folder FLASH_LED. Under Windows you should see the following project file content (see Figure 1-6). The project file content contains the C source (.C) and object code (.O), a MAP to show where code and data is assigned within the microcontroller memory, and an executable file (.HEX). The most important files, for our purposes at this time, are the project files (.MCP) and the workspace file (.MCW). Both of these last files are displayed with the MPLAB IDE logo. Double click the project icon marked .MCP file and MPLAB will reconstruct the project from the last stored workspace for that project. The workspace captures what windows are open, how the microcontroller is configured, and what debugging options were set. The workspace is captured with the .MCW file. Figure 1-6 captures the whole process.

![](img/a9229e7b0ddd9608f171b22b52514f39_19_0.png)

Let's continue with a closer look at the MPLAB contents using this project to gain a better appreciation of the MPLAB visual environment. In this project workspace there are several windows open. First is the overall Project Window, this window shows in tree structure all the associated user files or support files that are part of this project's source code build. Only two source code files appear here. You can examine any files contents by double clicking on the specific file within the Project Window. The other window that is open is the source code window (Figure 1-7).

Notice that this window is tabbed, in that all the source files within the project have been open for viewing, but only one file can be viewed at a time. You can alternate your source code views by clicking the associated tab aligned with the particular source code file. Another window visible in the workspace is the Output Window. The output window has many tabs and again you can alternate your views between debugger statuses, build/compile errors as well as several others (we will learn all of these features later in this book). Finally there is the MPLAB panel and tool bar on top of the main window. Here you can direct what operation you want the MPLAB to perform.

If you do not have your Microstick II connected at this time, the output window should indicate this (only because the Microstick II debugger was active as part of the original workspace configuration). Please connect your Microstick II at this time, if it hasn't been connected already. A Microchip USB driver is automatically installed the first time you hook up your Microstick II. Once done the Windows operating system should recognize the Microstick II connection automatically afterwards. Once the Microstick II is connected and driver installed the output window should respond that the debugger is connected. The Microstick II Debug LED should be constantly on.

![](img/a9229e7b0ddd9608f171b22b52514f39_22_0.png)

Figure 1-8: Building demo code

Now for execution, this is the absolute final step in the process. Here's where the payoff for all our hard work occurs. Let's review our status so far. We have a successful build, and the Microstick II is connected. Now let's simply program the device and run the debugger. This is a two-step process; again we have to direct our attention to the tool bar. Click program button, and then click the run button (Figure 1-9).

Build All Button

![](img/a9229e7b0ddd9608f171b22b52514f39_23_0.png)

Figure 1-9: Programming Microstick II

After clicking run the Microstick II should be running and the IDE should be responding with a visible activity bar active in the lower left hand corner of the IDE window. In addition, the run button on tool bar is disabled, and only the pause button is available for use. You can click pause button on the tool bar and the Microstick II will stop at the current line that the microcontroller was beginning to execute. A green arrow will appear in the source code window (if it is open) as to what line of source the microcontroller is paused at. You can then elect to run from there (click run), or use single step (click single step) to execute one line of source at a time, or reset (click reset) and the microcontroller will start execution of your code from the beginning.

It would help here to briefly cover some of the important debug functions, discussed so far, that reside in the IDE tool bar (see bullet items below and Figure 1-10):

- Make – just rebuild code that is new
- Build All – rebuild all code in Project Window
- Program the device ( in this case for debugging functions)
- Run –execute the program
- Pause- stop the program
- Single Step – execute one line of code from where you previously paused and then pause after execution.
- Reset –reset the device so the next run or pause execution will occur from beginning of code

![](img/a9229e7b0ddd9608f171b22b52514f39_24_0.png)

Congratulations –you now have a fully functional microcontroller development system! With this tool suite you can now undertake the exercises in this book and begin to progressively prepare and train yourself in 16 bit Microcontroller embedded design techniques.

We will be covering the function and features of MPLAB more carefully in the chapters to follow. Now let's discuss some of the important hardware features of the Microstick II and the PIC24H microcontroller so as to better understand these important resources and their full capabilities.

## Install Errors

- 1. Source Code Compile Errors-If compile errors occur you may have inadvertently typed or entered text in the source window and this would be accepted by the IDE as new code for the build. If this is the case close the IDE and do not save the workspace, reload the demo code and start again.
- 2. 'C' Compiler Not installed -If compile operation did not even occur, and the output window reports that it can't find the compiler; you may have overridden the default location for compiler. You now have one of two choices. The first choice is to just reinstall the compiler to its IDE default

digital controller operations, like motor control, digital power conversion, digital filtering. This series is marked with its own dedicated MAC or "Multiplier Accumulator Unit" in order to perform high speed math operations. This series also uses a 40 bit accumulator to insure there is no overflow of math operations. The dsPIC30 is a +5V part. The dsPIC33 is a +3.3V part. Microchip exclusively supplies its own signal processing and high speed math libraries for these parts free. For this book we will focus on experiments and operation for the PIC24H that can also be applied to understanding the PIC24F and dsPIC33.

The Microstick II is socketed and can support both the PIC32 (32 bit microcontrollers), PIC24H, PIC24F and dsPIC33 (16 bit microcontrollers) targets. It ships with the PIC32 in the socket. This needs to be removed and replaced with the PIC24H part. Our focus in this book is on the high end 16 bit microcontrollers not the 32 bit microcontroller. The socket only supports 28 pin Skinny DIP packages. Your Microstick II ships with four such devices, the PIC32MX220F032, the PIC24HJ128GP502, the dsPIC33FJ128MC802, and the PIC24FJ64GB002. All of these parts are +3.3VDC logic and have a similar pin out configurations. The PIC24H and dsPIC33 have memory capacities 128K Flash and 8K Ram and both can operate up to full rate of 40 Million Instructions per Second (MIPS). The PIC24H has a reduced memory capacity of 64K Flash and 8K Ram with a 32 MIPS rate.

![](img/a9229e7b0ddd9608f171b22b52514f39_26_0.png)

Figure 1-12: 16 Bit Microcontroller Support for Microstick II

Why use a Microchip 16 bit part? After all, the large variety of Microchip 8 bit parts have been around for a while and are all well supported. To facilitate this decision it may help to carefully review both performance and capability of a new 16 bit processor side by side with an 8 bit machine. A table is provided to
