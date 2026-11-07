The player then types a first guess. The program responds with one of the following:

+   1. Excellent! You guessed the number!\n   Would you like to play again (y or n)?\n2. Too low. Try again.\n3. Too high. Try again.

If the player’s guess is incorrect, your program should loop until the player finally gets the number right. Your program should keep telling the player Too high or Too low to help the player “zero in” on the correct answer.

# **6.35** *(Guess-the-Number Game Modification)*

Modify the program of Exercise 6.34 to count the number of guesses the player makes. If the number is 10 or fewer, print "Either you know the secret or you got lucky!" If the player guesses the number in 10 tries, then print "Ahah! You know the secret!" If the player makes more than 10 guesses, then print "You should be able to do better!" Why should it take no more than 10 guesses? Well, with each “good guess” the player should be able to eliminate half of the numbers. Now show why any number from 1 to 1000 can be guessed in 10 or fewer tries.

# **6.36** *(Recursive Exponentiation)*

Write a recursive function `power(base, exponent)` that, when invoked, returns\n\n$$\mathrm{power}(base, exponent)$$

For example, `power(3, 4) = 3 * 3 * 3 * 3`. Assume that exponent is an integer greater than or equal to 1. Hint: The recursion step would use the relationship\n\n$$base^{exponent} = base \cdot base^{exponent-1}$$\n\nand the terminating condition occurs when exponent is equal to 1, because\n\n$$base^1 = base$$

# **6.37** *(Fibonacci Series: Iterative Solution)*

Write a nonrecursive version of the function `fibonacci` from Fig. 6.29.

# **6.38** *(Towers of Hanoi)*

In this chapter, you studied functions that can be easily implemented both recursively and iteratively. In this exercise, we present a problem whose recursive solution demonstrates the elegance of recursion, and whose iterative solution may not be as apparent.

The **Towers of Hanoi** is one of the most famous classic problems every budding computer scientist must grapple with. Legend has it that in a temple in the Far East, priests are attempting to move a stack of golden disks from one diamond peg to another (Fig. 6.34). The initial stack has 64 disks threaded onto one peg and arranged from bottom to top by decreasing size. The priests are attempting to move the stack from one peg to another under the constraints that exactly one disk is moved at a time and at no time may a larger disk be placed above a smaller disk. Three pegs are provided, one being used for temporarily holding disks. Supposedly, the world will end when the priests complete their task, so there is little incentive for us to facilitate their efforts.

Let’s assume that the priests are attempting to move the disks from peg 1 to peg 3. We wish to develop an algorithm that prints the precise sequence of peg-to-peg disk transfers.

If we were to approach this problem with conventional methods, we would rapidly find ourselves hopelessly knotted up in managing the disks. Instead, attacking this problem with recursion in mind allows the steps to be simple. Moving n disks can be viewed in terms of moving only n − 1 disks (hence, the recursion), as follows:

+   a) Move n − 1 disks from peg 1 to peg 2, using peg 3 as a temporary holding area.\nb) Move the last disk (the largest) from peg 1 to peg 3.\nc) Move the n − 1 disks from peg 2 to peg 3, using peg 1 as a temporary holding area.