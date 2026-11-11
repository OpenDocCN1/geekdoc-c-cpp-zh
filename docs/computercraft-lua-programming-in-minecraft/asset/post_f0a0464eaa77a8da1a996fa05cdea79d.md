
Figure 5-2 shows the Computer terminal, which prompts for the message to be translated into dots and dashes (short and long flashes).

The program cannot translate all characters into Morse code; it can only do the upper and lowercase letters and the digits 0 to 9. It can also do a space, which is just a pause.

If you type in a character that it cannot translate, it will just ignore it.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_41_0.png)

Figure 5-2. Sending Commands to the Morse Code Sender.

Figure 5-3 shows the Morse Sender with the Redstone lamp lit.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_41_1.png)

Figure 5-3. The Morse Sender with the Redstone Lamp Lit.

### Software

The program is long enough not to want to type in, so see Appendix A, if you would rather download it.

The program uses two lists, one for letters and one for numbers.

```lua
letters = {
    ".-", "-...", "-.-.", "-..", ".", "..-.",
    "--.", "....", "..", ".---", "-.-", ".-..",
    "--", "-.", "---", ".--.", "--.-", ".-.",
    "...", "-", "..-", "...-", ".--", "-..-",
    "-.--", "--.."
}

numbers = {"-----", ".----", "..---",
    "...--", "....-", ".....", "-....", "--...",
    "---..", "----."}
```

Each element of the lists is a string of dashes and dots. A dash represents a long flash and a dot a short flash.

The *sendMorse* function is where most of the action takes place. It takes a single letter code and flashes it out as Morse.

By letterCode we mean a number that is used to represent that letter within Lua. Every letter has a number, so for example the letter A has a value of 65. The Lua code `string.byte("A", 1)` will return that letter code.

So the function handles the four possible types of letter, in the four if statements.

```lua
function sendMorse(letterCode)
    if letterCode >= string.byte("A", 1)
        and letterCode <= string.byte("Z", 1) then
        dashesAndDots =
            letters[letterCode-string.byte("A", 1)+1]
        for i = 1, string.len(dashesAndDots) do
            sendDashOrDot(string.byte(dashesAndDots, i))
        end
    end
    if letterCode >= string.byte("a", 1)
        and letterCode <= string.byte("z", 1) then
        dashesAndDots =
            letters[letterCode-string.byte("a", 1)+1]
        for i = 1, string.len(dashesAndDots) do
            sendDashOrDot(string.byte(dashesAndDots, i))
        end
    end
    if letterCode >= string.byte("0", 1)
        and letterCode <= string.byte("9", 1) then
        dashesAndDots =
            numbers[letterCode-string.byte("0", 1)+1]
        for i = 1, string.len(dashesAndDots) do
            sendDashOrDot(string.byte(dashesAndDots, i))
        end
    end
    if letterCode == string.byte(" ", 1) then
        sendDashOrDot(0)
    end
end
```

The first checks to see if it is between A and Z, the second between a and z, the third checks to see if it is a digit and the final check is for a space character.

Within each of these if statements there is a loop that goes through each letter of the dots or dashes in the code calling the *sendDashOrDot* function to actually control the Redstone.

```lua
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

This function also uses three if statements to work out if the flash to make is a small one for a dot, a long one for a dash or no flash at all for a space.

To make each flash, the Redstone first has to be turned on with the command *rs.setOutput("left", true)*, there is then a delay of half a second using the command *sleep*, before the Redstone is turned off again. Finally there is another 0.5 second delay.

If you wanted to make the flashing faster then you would need to decrease these delays.

The flash for a dash should be three times the flash length of a dot.

The main part of the program is outside of any function and will therefore just run when the program is run. This clears the terminal and prompts the user to enter a string to send.

```lua
term.clear()
term.setCursorPos(1, 1)
print("Enter Message to Send")
message = read()
```

It then loops over each letter in the string sending it to the function *sendMorse*.

```lua
for i = 1, string.len(message) do
    sendMorse(string.byte(message, i))
end
```

You could if you wish put everything from term.clear() into a while true loop so that you do not have to run the program each time you want to send a message.

### Summary

This is quite a tricky project to program, as you need to use arrays and manipulate strings to find the character codes of individual letters. You should find that if you can follow this code, you can do most things in ComputerCraft.

## CHAPTER 6: COMPUTER NETWORK

ComputerCraft will actually allow you to create more than one computer in a world and what is more, to connect the computers together in a network. To accomplish this you just need to add a couple of computers and attach wireless modems to the sides of them.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_46_0.png)

Figure 6-1. A Computer Network in ComputerCraft

In this project (Figure 6-1), there are two computers (one is hidden behind the screen in Figure 6-1), and you can type messages on the terminal in one computer and the message will be transmitted to the other computer where it will be displayed on the large screen attached to it.

### Setting Up the Sending Computer

In hardware terms, you just need a Computer and a wireless modem. Remember which side of the computer the wireless adapter is connected, as you will need to specify this in the program.

The program for the sender is called "sender" and can be downloaded with the other programs used in this book from https://github.com/simonmonk/computercraft_examples. See Appendix A for more information on installing the program. Alternatively, neither the sender nor the receiver is long, so they can easily be typed in.

Here is the full program for the sender.

```lua
while true do
  term.clear()
  term.setCursorPos(1, 1)
  print("Please enter message to send:")
  message = read()
  rednet.open("right")
  rednet.broadcast(message)
  rednet.close("right")
  sleep(0.1)
end
```

The program loops forever, waiting for a message to be entered. When a message is entered, then it opens a connection to the wireless network using rednet.open. The side passed as a parameter (in this case "right") needs to match the face of the computer to which the wireless access point is attached.

The command rednet.broadcast sends the message to all computers to which this computer is attached. Finally the connection is closed using rednet.close.

### Setting Up the Receiver

The receiver setup is the same as the sender, with the addition of a monitor on which the messages will be displayed.

The program for the receiver is still pretty simple. See Appendix A for details of how to download and install it, or you can enter it using the editor.

```lua
rednet.open("left")
while true do
  id, message = rednet.receive(1)
  if message then
    print(message)
  end
end
```

The first thing that happens is that a connection is established to the wireless access point to the left. There is then a loop that will only quit if you CTRL-T the program. Inside this loop rednet.receive is called to see if there is a message.

You will notice that there are two variables being assigned to the result of calling `rednet.receive` (id and message). This is because the function returns two values. The first value is the id of the computer that sent the message (this will be a number) and the second value is a string containing the message.

The if statement makes sure that a message was actually received before printing it.

When you start the receiving computer, remember to run it on the monitor by starting it with the command:

```
monitor right receiver
```

If your monitor is on some side of the computer other than right, then change this in the command above.

### Sending a Message

Start the receiver running as described above and then move over to the sending computer and start the sender program running (Figure 6-2).

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_48_0.png)

Figure 6-2. Sending a Message

Type in the message you want to send and hit Enter. If all is well the message will appear over on the receiving computer's monitor.

### Summary

There is nothing to stop you building bigger networks of computers and allowing them to send messages to each other. You could for instance have one control computer that
