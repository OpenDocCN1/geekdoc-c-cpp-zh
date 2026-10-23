# 9.5.3 Character Offset

A simple way to make it much harder for anyone to read what is in your file is to take the characters and offset them by a specified amount in the alphabet. The simplest code for doing this might look like the following.

```
val offset=args(2).toInt
mapFile(args(0),args(1),c=> (c+offset).toChar)
```

Here we convert the third argument to an Int and then add it to whatever character we are encrypting. This has to be turned back into a Char with toChar because doing arithmetic with the Char type implicitly results in an Int.

This is simple enough and works well for both encoding and decoding. To decode a message, simply use an offset that is the additive inverse of what you used originally. The only thing lacking in this is that letters can be shifted out of the alphabet making them look a bit odd when the text is printed. This problem can be resolved by having the characters wrap around the end of the alphabet. So if the offset would move the letter beyond 'z', it is wrapped back to 'a'. Similarly, we need to handle the case where the offset is wrapped before 'a'. The easy way to do this is with a modulo operator. The following code will work for any offset larger than -26.

```
val offset=args(2).toInt
mapFile(args(0),args(1),c=> {
  if(c.isLower) ('a'+(c-'a'+offset+26)%26).toChar
  else ('A'+(c-'A'+offset+26)%26).toChar
})
```

This code is a bit more complex because it has to differentiate between lowercase and uppercase letters so that it knows what to subtract from the character to get a value that we can take the modulo of.

This code also does something that might look a bit odd to you at first. The function literal now includes curly braces. Remember that the curly braces just make a code block, which is an expression whose value is the value of the last expression in the code block. This block only has one statement, an if expression, but putting it in a block helps to set it off and make it easier to read.

# 9.5.4 Alphabet Flip

A slightly different way to alter the letters is to flip the alphabet around. So a 'z' will become an 'a', a 'y' will become a 'b', and so on. This encoding does not need an extra argument for something like the offset. It also has an interesting side effect that the transformation is its own inverse. The code to do this might look like the following.

```
mapFile(args(0),args(1),c=> {
  if(c.isLower) ('a'+(25-(c-'a'))).toChar
  else ('A'+(25-(c-'A'))).toChar
})
```

This has the same basic structure of the normal offset version. It just does not need to get an offset and it uses an adjustment of 25 minus the characters position in the alphabet.