
```python
for k in user.keys():
  if k == "user":
    continue
    print "\t%s: %s" % (k,user[k])
```

And here's our output:
./pass.py password
User : ryan
uid : 1000
home : /home/ryan
name : Ryan
pass : R431
User : jason
uid : 1001
home : /home/jason
name : Jason
pass : J739
User : don
uid : 1002
home : /home/don
name : Don
pass : D831

We can see that there were users with default passwords in our sample.

We have gone over the basics of dictionaries, but dictionaries can be created in other ways. Fig. 2.7 shows two more examples of creating dictionaries that may be helpful.

```python
root@mostdefinitelynotkali:~/Desktop# python
Python 2.7.9(default Mar 1 2015, 12:57:24)
[GCC 4.9.2] on linux2
type 'help', 'copyright', 'credits' or 'license' for more information.
>>> dict(name='python', status=1337)
{'status': 1337, 'name': 'python'}
>>> dict([('python',1337),('pentesting','rawks')])
{'python': 1337, 'pentesting': 'rawks'}
>>> _
```

## FIGURE 2.7 Creating dictionaries.

On the first instance, we are specifying key-value pairs separated by commas. This is straightforward and similar to how we did it in our script. The second method uses a list of tuples, ordered pairs of information, passed to the dict function. Each key-value pair is enclosed in parentheses, letting the function know they should be grouped together. There is no best way to create a dictionary; some approaches may be easier in some cases, but the approach you use will mostly be a matter of aesthetics.

## Control Statements

We have encountered a number of control statement types in the scripts we have created thus far. There are other ways to control the execution of a script. In this section, we will look at conditionals and loops.

Conditionals are decision points that determine what part of our code to follow. The two most common ways to generate these statements are through comparison operators and functions that return either true or false. The comparison operators are going to be consistent with most other languages, but you can reference them in Table 2.1.

## Table 2.1 Python Conditional Operators

| Operator | Meaning | Operator | Meaning |
| --- | --- | --- | --- |
| < | Less than | > | Greater than |
| == | Equivalent | != | Not equivalent |
| <= | Less than or equivalent | >= | Greater than or equivalent |

## If statements

We have seen these conditionals in action throughout chapter, they have been used in simple if statements. Let's look at a more complex example.

```python
#!/usr/bin/python
import os
myuid = os.getuid()
if myuid == 0:
    print "You are root"
elif myuid < 500:
    print "You are a system account"
else:
    print "You are a regular user"
```

This code begins by getting the logged-user's ID from the operating system. It then checks to see if it is equivalent to 0. If it is, comparison returns true; it will print "You are root." The elif statement allows us to add extra conditionals within the same indentation. If none of our if and elif statements return true, the default condition is else. Now’s look at a modified example where we use a function that checks if we can read shadow file. We test this with os.access. We want to know if we can read the file, so we use constant os.R_OK to indicate that the file is readable. If we can read shadow file, eventually get the root password. This is what some penetration testers call. Otherwise, we will have to try something else.

```python
#!/usr/bin/python
import os
if os.getenv('USER') == "root":
    print "You are root"
elif os.getuid() == 0:
    print "You are sudo as root"
elif os.access('/etc/shadow', os.R_OK):
    print "You aren't root, but you can read shadow"
else:
    print "No soup for you"
```

## Loops

Loops are more useful for repeated actions. Two basic loop types are for loops and while loops. For loops iterate through a list and while loops until a condition is met or we break out of the loop. We used for loop in earlier scripts (e.g., pass.py), but we’t seen while loop yet:

```python
while 1:
    if i > 0 and i < 10:
        i = i + 5
        continue
    elif i % 2 == 0:
        print "EVEN"
    elif i % 3 == 0:
        print "ODD"
    elif i % 5 == 0:
        break
    print str(i+1)
```

This while loop will run forever because 1 is always true. Therefore, we will have to make sure there are conditions to break out of this loop; it will never stop on its own. Our first if statement checks to determine if variable i is between 1 and 9; if it is, we will add to it and continue. The continue operator says: “Stop here, and go to the next iteration of our loop.” Experiment with this script to see how adding other conditions can change the flow of the program.

## Functions

So far the scripts we have written are small. As we move on to larger programs with sections of code we want to reuse, functions become critical. Functions give us logical and reusable groupings of code. Functions begin with the def statement, followed by the name of the function and the list of arguments the function requires. Let’s look at a practical example.

Pen-testing will frequently advertise where all the goodies are without needing to ask. The robots.txt file where people can tell search engines where not to index are frequently the places we want to look when we are trying to find the interesting stuff. Here is a function that will get the robots file and give us the paths meant to find:

```python
def getDenies(site):
    paths = []
    # Create a new robot parser and read the site's robots file
    robot = robotparser.RobotFileParser()
    robot.set_url("http://"+site+"/robots.txt")
    robot.read()
    # For each entry, look at the rule lines and add the path to paths if disallowed
    for entry in robot.entries:
        for line in entry.rules:
            if not line.allowance and paths.append(line.path)
    return set(paths)
```

Our function, getDenies, takes one argument: site hosting the robots.txt file. This argument is required because it has no default value. We could make this value optional by adding an assignment operator and a default value. This would look like site = 'localhost' instead of the site variable. Once we have our site, we create a new RobotFileParser instance and set the URL to be the fully qualified path to the robots.txt file by using the set_url method. We use the read method to read the information into our parser which takes care of parsing all the data for us. Python uses indentation to determine context, so we know that our function has ended when our indentation returns to the same indentation as our function statement.

Now that we have the parsed data in our parser object, we are going to directly access the entry groupings it gathered. Each entry grouping is made of rule lines. We are going to use nested loops to get each individual line and then check if it is an "allow" or a "deny". We do this by checking the allowance variable, and if it is false we add the path to our paths list. Once we've gone through all the rule lines, we will use the set function to consolidate all the duplicates in our list into a single list of unique elements. Finally, our return function gives that information back to the calling code. Not all functions have to have a return value.

Now that our function is complete, we can generate the rest of the code that is necessary to make our program useful:

```python
import robotparser
sites = ['google.com']
```

## File Manipulation

While there are other programming languages that excel at file parsing (such as Perl), sometimes it will be more convenient to perform file manipulation in Python. In this section, we will go over the basics of reading and writing to files. We have read from files before, when we created pass.py using the open command and specified the file as readonly. There are a few modes we need to know.

In addition to the r or read mode, there is the w mode for write, and a mode for append. Two important modifiers for these are + and b. The + indicates that, in addition to the mode you chose, the file will be writable. The w mode overwrites the filename with a blank file when it opens. The b flag isn't used in UNIX, but in Windows it indicates that the file should be a binary file. To read and write a binary file in Windows you would use r+b.

Once the file is open, the read and write functions come into play. There are three primary read methods: read, seek, and tell. The read method reads from the file. If no argument is passed to read, it will read the whole file and return information as a string. If your file is massive, this may be a problem. So, you can specify a number of bytes to read, and read will return only the number of bytes or an empty string if you are at the end of file. The readline method returns an entire line as a string, and readlines function returns the entire file as a list of strings.

The final two methods that may use are seek and tell. These come into play particularly when you are dealing with binary files. The tell method tells you what your position is in the file, and the seek function allows you to move forward or backward in a file based
