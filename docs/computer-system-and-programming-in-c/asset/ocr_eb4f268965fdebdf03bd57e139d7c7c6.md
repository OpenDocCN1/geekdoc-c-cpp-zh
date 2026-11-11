![](bbox=[0.145, 0.094, 0.401, 0.303])

The for loop begins with a loop control variable assigned a specific initial value. This control variable is then incremented (or decremented) by a specified amount each time around the loop until a specified terminating value is reached at which time the statement following the loop is then executed.

The pseudocode of the above construct is as follows:
for (initial-value, final-value, increment)
statement-1

# Example

for (a = 3, a > 12, a = a + 2)
print a
The above code segment will print 3 5 7 9 11.

# While Loop

A while loop allows a statement to be executed until a given condition is met. If the condition is met prior to executing the loop then the loop will not be executed. As soon as the condition is met, execution continues with the statement following the loop. Graphically it is represented as follows:

![](bbox=[0.145, 0.725, 0.404, 0.934])

The pseudocode of the above construct is as follows:
while not condition
statement-1

# Example

while not end-of-file
{
read record
write record
}

# Do Until Loop

An until loop also allows a statement to be executed until a given condition is met but the condition will not be tested until after the loop has been executed once. Once the condition is met the statement following the loop will be executed. Graphically it is represented as follows:

![](bbox=[0.591, 0.434, 0.839, 0.655])

The pseudocode of the above construct is as follows:
do
statement-1
until condition

# Advantages of Structured Programming

The following are the advantages of structured programming:

+   - The foremost advantage is reduced complexity.
+   - Modularity allows the programmer to tackle problems in a logical fashion.
+   - Also, the use of logical structures ensures that the flow of control is clear.