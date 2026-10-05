```
case "Include":
echo "Perform activities for including.";
echo "The greatest number of statements as you like can be in every piece.";
break;
case "MODIFY":
echo "Perform activities for modifying.";
break;
case "Erase":
echo "Perform activities for erasing.";
break;
}
```

The switch statement lives up to expectations by taking the value after the switch keyword and comparing it to the cases in the order in which they are arranged. If no case matches, the code isn't executed. When a case matches, the code is executed. The code in consequent cases additionally executes until the end of the switch statement or until a break keyword. This is helpful for procedures that have chronological steps. If the client had done several steps, he can resume the process where he left off.

The expression after the switch statement must assess to a simple type e.g. integer, a string or a number. An array can be utilized just if a specific individual from the cluster is referenced as a simple type.

There are various approaches to direct PHP not to execute cases other than the matching case.