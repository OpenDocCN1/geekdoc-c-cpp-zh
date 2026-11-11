will be printed to the display.

You already possess the required knowledge to do all of this yourself, so before you go through the example you should try to develop your own program. With that in mind, it would look something like this:

```
~~~text
myFile.py

Problem: Generate information on roleplaying characters

Target audience: Personal / Friends and family

System: Windows / Linux

Interface: Command Line

Functional requirements: Print a character sheet.

User will input name, gender, race and description.

Test: Basic execute test.
~~~
```

```
~~~python
Name = ''

Gender = ''

Race = ''

Description = ''

# Prompt user for information

Name = input('what is your name? ')
Gender = input('what gender are you? (male / female / not sure): ')
Race = input('what race are you? (Human / Elf / Orc / Dwarf / Gnome): ')

# Output character sheet

cool_line = '<_==|#=--+--+*$/*+--+--=#|==_>'
~~~
```