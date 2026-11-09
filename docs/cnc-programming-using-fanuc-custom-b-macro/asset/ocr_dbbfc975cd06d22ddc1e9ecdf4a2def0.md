# ## Execution Pause

System variable #3009 generates an alarm condition and terminates the program execution, whereas variable #3006 causes temporary pause of execution, which can be restarted by pressing the CYCLE START button again. In the paused state, pressing the MESSAGE key displays the user-specified message (up to 26 characters). Assigning a number to variable #3006 halts the program execution. There is no significance to this number, because message number is not displayed. So, normally, 1 is assigned. Example:

```
```text
#3006 = 1 (CHECK THE DIAMETER);
```
```

This would temporarily stop the execution, and display “CHECK THE DIAMETER” on the message screen. If no message is typed, nothing would be displayed.

# ## Mirror Image Information

Apart from programmable mirror image command, it is also possible to obtain mirror image profiles using external switches on the MOP (there are separate switches for different axes), or through the mirror image setting screen. (Select MDI mode → Press OFS. SET function key → Press SETING soft key → Now, after pressing page down key, the mirror image screen will appear, on which select I for activating the mirror image for a particular axis.)

The mirror image status of each axis is stored in a read-only system variable #3007. For a bit-type variable, but it stores the value in decimal form. For example, 00000011 (where 1 indicates mirror image enabled and 0 indicates mirror image disabled) is stored as 3. So, the value stored in this variable needs to be converted into binary for interpreting it. For example, a value of 3 indicates that mirror image is enabled for the first two axes. Table 3.9 shows the bit settings for this variable.

On a lathe, the first and the second axes refer to the X- and Z-axis, respectively, and on a milling machine, the first three axes refer to the X-, Y-, and Z-axis, respectively. Additional axes may or may not be available on a particular machine. Only the first four bits of this variable are used for the Fanuc 0i series.

# ## Number of Machined Parts

The number of parts required and the number of completed parts in the current machining session can be read or written in system variables.

| Bit #7 | Bit #6 | Bit #5 | Bit #4 | Bit #3 | Bit #2 | Bit #1 | Bit #0 |
|---|---|---|---|---|---|---|---|
|  |  |  |  | 4th axis | 3rd axis | 2nd axis | 1st axis |

Table 3.9  Bit Settings for System Variable #3007