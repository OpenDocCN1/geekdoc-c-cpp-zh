# Programming Projects 823

Write a program that implements the previous maze using references to instances of a Node class. Each node in the graph will correspond to an instance of Node. The edges correspond to links that connect one node to another and can be represented in Node as instance variables that reference another Node. Start the user in node A. The user's goal is to reach the finish in node L. The program should output possible moves in the north, south, east, or west direction. Sample execution is shown next.

You are in room A of a maze of twisty little passages, all alike. You can go east or south.

E
You are in room B of a maze of twisty little passages, all alike. You can go west or south.

S
You are in room F of a maze of twisty little passages, all alike. You can go north or east.

+   12. First, complete Programming Project 17.11. Then, write a recursive algorithm that finds a path from node A to node L. Your algorithm should work with any pair of start and finish nodes, not just nodes A and L. Your algorithm should also work if there are loops such as a connection between nodes E and F.