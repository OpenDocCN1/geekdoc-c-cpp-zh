# 8.12 THE STICKS PROGRAM

All of the basic techniques needed for completing the Sticks program have been discussed. The complete listing of the Sticks program is in the file sticks.clp, found on the CD-ROM packaged with this book. A sample run of the program after it has been loaded is shown below:

```
CLIPS> (reset).]
CLIPS> (run).]
Who moves first (Computer: c Human: h)? c.]
How many sticks in the pile? 15.]
Computer takes 2 stick(s).
13 stick(s) left in the pile.
How many sticks do you wish to take? 3.]
10 stick(s) left in the pile.
Computer takes 1 stick(s).
9 stick(s) left in the pile.
How many sticks do you wish to take? 2.]
7 stick(s) left in the pile.
Computer takes 2 stick(s).
5 stick(s) left in the pile.
How many sticks do you wish to take? 1.]
4 stick(s) left in the pile.
Computer takes 3 stick(s).
1 stick(s) left in the pile.
You must take the last stick!
You lose!
CLIPS>
```

# 8.13 THE OR CONDITIONAL ELEMENT

Thus far all the rules shown have an implicit and conditional element between the patterns. That, is a rule will not be triggered unless all the patterns are true. CLIPS also provides the capability of specifying both an explicit and conditional element and an explicit or conditional element on the LHS.

As an example of an or CE, consider the following rules for use by the industrial plant monitoring system (as discussed in Chapter 7) that are first written without an or CE. Then you will see how to rewrite them with an or CE:

```
(defrule shut-off-electricity-1
(emergency (type flood))
=>
(printout t "Shut off the electricity" crlf))
```