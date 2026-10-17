To sort the element the radix sort involves a group of pockets which are numbered from 0 to 9.

These pockets can accept numbers whose lsd is equal to the respective pocket numbers.

For example 0ᵗʰ pocket can accommodate only elements that end with 0. Similarly, pocket no 5 accommodates elements whose lsd is 5 and each pocket can accommodate only one element per pass Step I In the first step the list is traversed and elements are placed in the pockets based on their lsd.

Once an element is placed in its respective pocket of another element with the same lsd is encountered it is ignored until the rest of the list is scanned. This scanning through a list once is called a pass.

For example in the above list you have two elements 40 and 50 having lsd as 0. In the first pass only 40 is placed in the 0ᵗʰ pocket since it is encountered first. The 50 is placed in the 0ᵗʰ pocket in the second pass.

Hence after the completion of the first step the elements can be represented as follows: P

0 40 50 1 61 2 72 3 4 5 45 6 7 67 57 8 9

Now based on the arrangement a new list is prepared as follows:

40, 50, 61, 72, 45, 67, 57

You will notice that while a list is prepared the element in the 2ⁿᵈ pass slides beside the element in the 1ˢᵗ pass.

This list of elements is now used as fuel for the second step.

Step II is similar to Step I with a variation that these elements are entered into their respective pockets based on the msd. 0 1 2 3 4 40 45 5 50 57 6 61 67 7 72 8 9. Hence the new ordered list can be represented as follows:

40, 45, 50, 57, 61, 67, 72.

After having dealt with the various sorting techniques it is difficult to judge which technique is the most superior one. Though some are easy to use it may not really be effective.

Certain properties of a given key set play an important role in the determination of which sorting technique should be used. The properties are the number, size, distribution, and order of keys. Often decide which method will be apt in a situation.