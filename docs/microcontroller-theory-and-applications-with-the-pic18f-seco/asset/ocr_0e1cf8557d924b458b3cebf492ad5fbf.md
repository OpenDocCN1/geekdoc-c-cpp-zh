```
MOVWF 0x32; # 34 are 16 hex digits
MOVWF 0x33; Move 16 to 0x33
DECF 0x33,F; Decrement 0x33 by 1 to contain hex digits F to 0
LFSR 0,0x50; # 35 Initialize FSR0 with 0x50
MOVF 0x31,W; # 36 Move row code to WREG
SEARCH CPFSEQ POSTINC0; # 37 Compare and skip if equal
BRA SEARCH1; # 38 Load if not found
MOVFF 0x33, PORTB; # 39 Get character along with LOW enable
BRA NEXT1; # 40 Branch to NEXT1
SEARCH1 MOVFF 0x31,W
DECF 0x33,F; Decrement 0x33
DECF 0x32,F; Decrement 0x32
NEXT1 GOTO SCAN_KEY; #41 Branch to SEARCH if not 0
DELAY MOVLW D'10'; Return to scan another key
MOVWF 0x20; 20 ms delay routine
LOOP1 MOVLW D'255'; LOOP2 provides 2 ms delay
MOVWF 0x21
LOOP2 DECFSZ 0x21;
GOTO LOOP2;
DECFSZ 0x20;
GOTO LOOP1;
RETURN;
END
```

In the program, a decode table for keys 0 through F are loaded into data memory using the MOV LW instruction starting at address 0x50 (chosen arbitrarily). The codes for the hexadecimal numbers 0 through F are obtained by inspecting Figure 9.19. For example, consider key 9. When key 9 is pressed and if a LOW is outputted by the program to bit 0 of PORTC, the second row and second column of the keyboard will be LOW. This will make the content of PORTD:

Bit Number: Bit 7 Bit 6 Bit 5 Bit 4 Bit 3 Bit 2 Bit 1 Bit 0
Data: 1 1 0 1 1 0 1 1 = DB16

Thus, a code of DB16 is obtained at PORTD when key 9 is pressed. Diodes are connected at the 4 bits (bits 0-3) of PORTC. This is done to make sure that when a 0 is output by the program to one of these bits (row of the keyboard), the diode switch will close and will generate a LOW on that row.

Now, if a key is pressed on a particular row that is LOW, the column connected to this key will also be LOW. This will enable the programmer to obtain the appropriate key code for each key. Next, the assembly language program will be explained using some of the line numbers included in the comment field.

Line #1 is the starting address of the program at 0x100. This address is chosen arbitrarily. Line #2 equates label OPEN to data 0xF0. This is because when all keys are up (no keys are pushed) and 0's are outputted to the rows via PORTC in Figure 9.19, data input at PORTD will be 11110000 (0xF0). Note that bits 0 -3 of PORTD are connected to rows and bits 4-7 of PORTD are connected to columns of the keyboard.

Line #3 and #4 store code for F, and are the start of the codes while Line #5 is the end of codes.