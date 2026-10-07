# COMMON CONCURRENCY PROBLEMS

| Application | What it does | Non-Deadlock | Deadlock |
|---|---|---|--|
| MySQL | Database Server | 14 | 9 |
| Apache | Web Server | 13 | 4 |
| Mozilla | Web Browser | 41 | 16 |
| OpenOffice | Office Suite | 6 | 2 |
| Total | | 74 | 31 |

Figure 32.1: Bugs In Modern Applications

were not deadlock (74); the remaining 31 were deadlock bugs. Further, while you can see the number of bugs studied from each application; while OpenOffice only had 8 concurrency bugs, Mozilla had nearly 60.
We now dive into these different classes of bugs (non-deadlock, deadlock) a bit more deeply. For the first class of non-deadlock bugs, we use examples from the study to drive our discussion. For the second class of deadlock bugs, we discuss the long line of work that has been done in it preventing, avoiding, or handling deadlock.

# 32.2 Non-Deadlock Bugs

Non-deadlock bugs make up a majority of concurrency bugs, according to Lu's status. But what types of bugs are these? How do they arise? Can we fix them? We now discuss the two major types of non-deadlock bugs by Lu et al.: atomicity violation bugs and order violation bugs.

# Atomicity-Violation Bugs

The first type of problem encountered is referred to as an atomic violation. Here is a simple example, found in MySQL. Before reading the explanation, figuring out what the bug is. Do it!

```
Thread 1:
if (thd->proc_info) {
  fputs(thd->proc_info, ...);
}

Thread 2:
thd->proc_info = NULL;
```

Figure 32.2: Atomicity Violation (atomicity.c)

In the example, two different threads access the field proc_info in the structure thd. The first thread checks if the value is non-NULL and then prints its value; the second thread sets it to NULL. Clearly, if the first thread performs the check but is then interrupted by the call to fputs, the second thread could run in-between, setting the pointer to NULL; when the first thread resumes, it will crash, as a NULL pointer will be dereferenced by fputs.