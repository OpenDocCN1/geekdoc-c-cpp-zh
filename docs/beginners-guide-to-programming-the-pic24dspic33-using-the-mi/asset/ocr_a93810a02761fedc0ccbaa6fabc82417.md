+   - 0.025" Pin headers – Enables plug-in to Breadboard with room for jumper wires
+   - Easy access to all device signals for probing
+   - Small size - Smaller than a stick of gum at 20 x76mm – Easily Portable
+   - On board debug LED, Utility LED and Reset Switch

# Review of 16 bit Experimenter Key Features:

+   - Plug in Module Format with built in 3.3V regulator for use with larger Solderless Breadboards.
+   - 16x3 low profile LCD display and 4 user defined pushbuttons
+   - ICSP interface for in circuit programming and debug
+   - Standard I/O Expansion Bus for breadboard access to PIC24H peripheral set
+   - On board 32KHz timing crystal for accurate timekeeping
+   - On board 32KB EEPROM

# Special Notes for Using dsPIC33 or PIC24F

+   1. Remove in the source code (typically resident before Main function ) the #include "p24hxxxx.h". Replace it with either #include "p33Fxxxx.h" for the dsPIC33 or #include "p24Fxxxx.h" for the PIC24F.
+   2. Use MPLAB IDE Configure Menu selection to select the exact dsPIC or PIC24F part you want to use.
+   3. Save, rebuild project, and run.

# Exercises :

+   1. What are some of key tools supported by the MPLAB environment?
+   2. What is meant by ICSP? And how is it used by the Microstick II?
+   3. Gain familiarity with Microchip's 16 bit family of products and target applications. Go to and review the materials at Microchip web site http://www.microchip.com/en_US/family/16bit/
+      a. What are some applications?