# CHAPTER 3  Scalars and Strings

![](bbox=[0.391, 0.109, 0.826, 0.231])

**Figure 3.18**  
The block is displayed with a print command.

# Blocks and Variables

Printing blocks can prove a useful way to handle large bodies of text immediately, but an equally beneficial use of blocks involves assigning them to scalar identifiers. You can assign blocks to scalar variables and then use the identifiers later. Parentheses enclose the assignment statement. Listing03_20 shows a basic approach to storing a block in a scalar variable and then printing the block afterward.

```
```text
#Listing03_20

#Blocks assigned to and used with variables

#Variable to be combined with block
$TestValue = "Mr. Blue";

($BlockVariable = <<NOTES);
    Thank you for contacting us.
    A service representative will
    contact you within 24 hours.
NOTES

#Concatenating a value with the block
print "\n \n" . " $TestValue,\n" . $BlockVariable;
```
```

Figure 3.19 illustrates the block displayed as output.

![](bbox=[0.39, 0.739, 0.826, 0.884])

**Figure 3.19**  
A block makes printing the notification convenient.