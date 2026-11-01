# Chapter 8

# Lists

# 8.1 Objective

+   - Understand what lists are
+   - Understand how assignments with mutable types work
+   - Access individual elements and slices in a list
+   - Iterate over lists with for
+   - Use common lists built-in functions
+   - Construct new empty lists of repeating fixed values
+   - Construct new lists with list comprehensions
+   - Construct and use lists of lists (2D lists)

# 8.2 Chapter Project Specification

Game time!

Allow the user to navigate a maze by entering directions to move (n, s, w, or e). They can also enter q to quit.

The maze should look like this, with . representing a space the player can move into, and # representing a wall. An @ symbol indicates the player’s current position.

Every move, the map should be displayed:

```
###################
#...#...........#
#...#...........#
#...#...#...#...#
#...#...#...#...#
#...# @ ...#...#
#...#...........#
#...#...........#
###################

Enter a move (n,s,w,e,q):
```

Keep this project in mind as you read through the chapter.

# 8.3 What Are Lists?

Problem-solving step: Understanding the Problem.

Remember how regular variables hold one thing? Well, lists are variables that can hold a lot of things.