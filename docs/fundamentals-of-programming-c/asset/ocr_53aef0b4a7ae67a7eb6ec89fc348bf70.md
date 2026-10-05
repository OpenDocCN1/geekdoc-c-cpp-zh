# 19.2. EXCEPTION EXAMPLES

![](bbox=[0.296, 0.191, 0.703, 0.383])

Figure 19.1: Function call chain without an exception. The vector<int>::at method, the find function, and the process function complete all their work and return as usual to their callers.

```
Creating Tracker (global)
------[Entering main]------
Creating Tracker (main)
------[Entering process]------
Creating Tracker (process)
Enter a range: 10 20
------[Entering find]------
Creating Tracker (find)
Enter item to locate: 4
Destroying Tracker (find)
Destroying Tracker (process)
nums vector bounds exceeded
------[Leaving main]------
Destroying Tracker (main)
Destroying Tracker (global)
```

The supplied range of 10..20 is outside the bounds of main's nums vector. Because the program does not print find message we know the find function does not complete its execution as usual. This is because the vector<int>::at method called by find throws an exception. Furthermore, it does not appear that find returns normally, since process does not print its exit message. We do see, though, that the program properly destroy the local Tracker objects owned by find and process. The program's execution path lands immediately back in main, which we see does exit normally after executing the statement in its cat.ch block. The program finishes by destroying main::Tracker object followed by destroying the global Tracker object. Figure 19-2

©2014 Richard L. Halterman

Draft date: January 26, 2014