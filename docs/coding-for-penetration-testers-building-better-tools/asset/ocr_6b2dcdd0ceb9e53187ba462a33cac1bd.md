# Variables

Perl, of course, also has a number of data structures we can use to store things, the more common among them being the scalar variable. Variables in Perl are always addressed with a $, whether altering the contents or simply reading them, and we can use a variable to store and manipulate a variety of content without having it to be of a particular type, as a string or integer. We can make use of variables in this simple script:

```
#!/usr/bin/perl
print "Hi. What is your name?\\n";n$name = <STDIN>; #take in a name
chomp $name;
print "$name is a nice name\\";
```

We used a variable here, and a couple of other things as well, let's walk through them. We use the shebang on the first line, as usual, that we use the proper interpreter. On the second line, we echo out a string to ask for a name. The next line defines our variable, $name, and waits for input from standard input, <STDIN>, which is the console where we will type when the script runs. This will place whatever we type at the console, until we press Enter, into our variable. Also notice our comment at the end of the line, starting with a pound sign, #. This will prevent the rest of the line from being interpreted when the script runs.

The next line makes use of chop, a very handy Perl function. When we took the input from <STDIN>, we edited it by pressing Enter. The newline represented by Enter (also known as \n) was also fed into our variable, and will show in our last output statement if we don't get rid of it, which is what chop does. While chop is specific to the newline, we could have also used chop, which will get rid of the last character, whatever it happens to be.

The last line of our script will echo out a compliment and make use of the data we stored in $name.

# Shell Commands

Another interesting and very handy tool we can make use of is the