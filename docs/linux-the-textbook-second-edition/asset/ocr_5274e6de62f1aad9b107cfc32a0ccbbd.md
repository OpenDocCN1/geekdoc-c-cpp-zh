# F₂ = 1

# Fₙ = Fₙ₋₁ + Fₙ₋₂, for n ≥ 3

Thus, the first ten numbers in the Fibonacci series are 0, 1, 1, 2, 3, 5, 8, 13, 21, and 34.

The script in the num_array_demo file is well documented and fairly easy to understand. It displays the sum of the first ten Fibonacci numbers. A sample run of the script follows the code.

```
$ cat num_array_demo
# File Name:
# Author:
# Date Written:
# Last Modified:
# Purpose:
# Brief Description:
#!/bin/bash -xv
# Initialize Fibonacci array to any number of Fibonacci numbers; first 15
# in this case.
declare -a Fibonacci=(0 1 2 3 5 8 13 21 34 55 89 144 233 377)
size=${#Fibonacci[@]}
index=1
sum=0
next=0
while [ $index -le $size ]
do
  next=${Fibonacci[$index]}
  sum=$((sum + next))
  index=$((index + 1))
done
echo "The sum of first ${#Fibonacci[@]} Fibonacci numbers is $((sum))."
exit 0
$ ./num_array_demo
The sum of first 15 Fibonacci numbers is 986.
```



Write a Bash script that contains two numeric arrays, array1 and array2, initialized to the values in the sets {1, 2, 3, 4, 5} and {1, 4, 9, 16, 25}, respectively. The script should produce and display an array whose elements are the sum of the corresponding elements in the two arrays. Thus, the first element of the resultant array is 1 + 1 = 2, the second is 2 + 4 = 6, and so on.



Replicate all Bash sessions and scripts discussed in this section on your system to verify that they produce expected results.



The here document feature of Bash allows you to redirect standard input of a command in a script and attach it to data within the script, wrapped in a particular format, as will be explained. Obviously, this feature works with commands that take input from standard input. The feature is used mainly to display menus, although there are some other important uses of this feature. The advantage of maintaining data within the script is that it eliminates extra file operations such as open and read that would be required if the data was maintained in a separate file. The result is a much faster program. The following is a brief description of the here document.