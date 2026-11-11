```
```text
sendDashOrDot(string.byte(dashesAndDots, i))
    end
end
if letterCode == string.byte(" ", 1) then
    sendDashOrDot(0)
end
end
```
```

The first checks to see if it is between A and Z, the second between a and z, the third checks to see if it is a digit and the final check is for a space character.

Within each of these if statement there is a loop that goes through each letter of the dots or dashes in the code calling the *sendDashOrDot* function to actually control the Redstone.

```
```text
function sendDashOrDot(dashOrDot)
    if dashOrDot == 46 then
        rs.setOutput("left", true)
        sleep(0.5)
        rs.setOutput("left", false)
        sleep(0.5)
    elseif dashOrDot == 45 then
        rs.setOutput("left", true)
        sleep(1.5)
        rs.setOutput("left", false)
        sleep(1.5)
    elseif dashOrDot == 0 then
        sleep(3)
    end
end
```
```

This function also uses three if statements to work out if the flash to make is a small one for a dot, a long one for dash or no flash at all for a space.

To make each flash, the Redstone first has to be turned on with the command *rs.setOutput("left", true)*, there is then a delay of half a second using the command *sleep*, before the Redstone is turned off again. Finally there is another 0.5 second delay.

If you wanted to make the flashing faster then you would need to decrease these delays.

The flash for a dash should be three times the flash length of a dot.

The main part of the program is outside of any function and will therefore just run when the program is run. This clears the terminal and prompts the user to enter a string to send.