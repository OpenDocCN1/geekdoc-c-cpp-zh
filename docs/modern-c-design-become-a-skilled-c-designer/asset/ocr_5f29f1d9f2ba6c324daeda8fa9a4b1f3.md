return type in the virtual interface.
Covariance allows a cloning function to always return the specific type appropriate to the hierarchy level from which cloning was called. This feature is important for implementations that have public cloning functions and allow cloning calls to be made from all levels in the hierarchy.

I chose to round out the command interface with a help message function and a corresponding virtual implementation function. The intent of this help function is to enforce that individual command implementers provide brief documentation for the commands that can be queried through a help command in the user interface. The help function is not essential to the functionality of the commands, and its inclusion as part of the design is optional. However, it’s always nice to provide some internal documentation for command usage, even in a program as simplistic as a calculator.

Combining all of the above information, we