# 2.4.3 Build the Project

After typing the code from the previous sub-section, build the project using the Build icon on the toolbar, or use Build ▶ Build led_blink_c from the top menu. If there are no errors in the code, the project will build and a message “Build succeeded.” appears in the window that pops up at the bottom of Microchip Studio.

# 2.4.4 Fix Any Build Errors

If the project did not build successfully, an error message, or error messages, will appear at the bottom of Microchip Studio, with a red X icon next to them. If this is the case, check that the code from the listing was entered exactly as shown. There is not much that can go wrong with this simple program, so just check for typographical errors, particularly look for semicolons left off and spelling errors. The source code for all programs in this book is available for download from Elektor. If there are still problems, download the code and copy and paste the code for this exercise into the main.c file of this Microchip Studio project. Save the changes and build again.

# 2.4.5 Load the Program to the AVR Microcontroller

The steps for loading the program to the ATtiny device are exactly the same for this C code project as for the assembly language project. For directly supported programmers, such as the Atmel-ICE, select your programming device, by clicking the None icon on the toolbar. Use the page that opens to select the programming device and the ISP interface, remembering that the programmer must be plugged into the USB port of the PC to appear in the selection list. Save the changes and then either click the Start Without Debugging icon on the toolbar, or use the keyboard shortcut Ctrl + Alt + F5, or select Debug ▶ Start Without Debugging from the top menu. For more details, refer back to section 2.3.5. For hobby programmers, click the programming button that you set up in Appendix A, assuming that you are using the same AVR part and programmer as for the assembly language program. If there are no problems, the program will load to the ATtiny and the LED will start blinking at a slower rate than for the assembler program.

# 2.4.6 Fault Finding

If there are problems loading the program to the microcontroller, refer back to section 2.3.6 for information on what can be done to resolve problems. Although section 2.3.6 is written for assembly, fault finding techniques are the same for a C program.