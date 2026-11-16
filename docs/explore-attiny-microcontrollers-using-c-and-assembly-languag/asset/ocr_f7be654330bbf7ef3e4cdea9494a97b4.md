instructions for a particular architecture. Download the AVR instruction set manual from Microchip at the following link and save it for reference when writing assembly programs.

ww1.microchip.com/downloads/en/DocDoc/AVR-Instruction-Set-Manual-DS40002198A.pdf (Search the internet for "AVR instruction set manual" if this link changes and does not work, or to find if a newer version of the manual is available)

Not all AVR assembly instructions are implemented in every AVR microcontroller. The ATtiny25/45/85 and ATtiny13(A) microcontrollers use a subset of 123 instructions from the entire AVR instruction set. The instructions available in these microcontrollers can be found in the ATtiny25/45/85, ATtiny13 and ATtiny13A datasheets at the links shown below. Look in the "Instruction Set Summary" section of any datasheet to see a list of implemented instructions. Download the datasheet or datasheets for the device or devices that you are using. Keep these datasheets for reference while doing AVR assembly language programming.

+   - **ATtiny25/45/85 datasheet:** ww1.microchip.com/downloads/en/deviceDoc/atmel-2586-avr-8-bit-microcontroller-attiny25-attiny45-attiny85_datasheet.pdf (Search the Internet for "ATtiny25 datasheet" if this link changes and does not work)
+   - **ATtiny25 web page:** www.microchip.com/en-us/product/ATTiny25
+   - **ATtiny45 web page:** www.microchip.com/en-us/product/ATTINY45
+   - **ATtiny85 web page:** www.microchip.com/en-us/product/ATTiny85
+   - **ATtiny13 datasheet:** ww1.microchip.com/downloads/en/DeviceDoc/doc2535.pdf (Search the Internet for "ATtiny13 datasheet" if this link changes and does not work)
+   - **ATtiny13 web page:** www.microchip.com/en-us/product/ATTiny13
+   - **ATtiny13A datasheet:** ww1.microchip.com/downloads/en/DeviceDoc/ATTiny13A-Data-Sheet-DS40002307A.pdf
+   - **ATtiny 13A web page:** www.microchip.com/en-us/product/ATTiny13A

There are some discrepancies about the number of instructions implemented in various AVR parts in the Microchip / Atmel datasheets. This is discussed towards the end of the book in section 11.3.1 of Chapter 11.