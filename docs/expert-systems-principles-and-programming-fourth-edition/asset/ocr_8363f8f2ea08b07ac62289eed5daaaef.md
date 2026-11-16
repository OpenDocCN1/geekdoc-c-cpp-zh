memory, one of six megabytes and another of four megabytes, and an application was launched that required four megabytes, then the application should be placed in the four-megabyte free block rather than the six-megabyte free block. When a launch or terminate command is processed, a message should be printed. If there is not a large enough memory block to launch a program, then a message to this effect should be printed. Test your program by asserting the preceding facts and issuing a run command after each program. The output should be similar to the following:

+   Application word-processor memory location is 1 to 2.
+   Application spreadsheet memory location is 3 to 8.
+   Unable to launch application game.
+   Terminating word-processor.
+   Application game memory location is 1 to 1.
+   Terminating spreadsheet.
+   Terminating game.

# 9.15 Develop a text menu interface that is self-contained within a module and is suitable for reuse in other programs.

The menu items should be represented as facts. Two types of actions should supported for menu items. One is to quit execution of the program. If this item type is selected, the program should halt execution. The other is to assert a fact and focus on a specific module. For this action, the menu-item facts should contain slots that specify the focus module and fact value to be asserted when the item is selected. For example, in the following dialog the result of selecting “Option A” would be to focus on module A and assert the fact (menu-select (value option-a) contains the appropriate values specified in the menu-item fact. Module A contains a rule that activates on the menu-select fact causing the “Executing Option A” message to be printed.

```
CLIPS> (run)
Select one of the following options:
1 – Option A
2 – Option B
9 – Quit Program
Your choice: 1
Executing Option A

Select one of the following options:
1 – Option A
2 – Option B
9 – Quit Program
Your choice: 9

CLIPS>
```