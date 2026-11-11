```
```python
file.write(file_text)
file.write("\n")
file.close()
fileText = real_input("Enter filename: ")
if len(fileName) == 0:
    print "Next time input something"
    sys.exit()
try:
    file = open(fileName, "r")
except IOError:
    print "Error reading file requested"
    sys.exit()
fileText = file.read()
file.close()
print fileText
```
```

# Multiple Line Statements

These statements normally terminate with a new line. Though, it allows you to use a special character (\) to continue a statement. Check the code below:

```
```python
Total_Number = number1 + \
    number2 + \
    number3
```
```