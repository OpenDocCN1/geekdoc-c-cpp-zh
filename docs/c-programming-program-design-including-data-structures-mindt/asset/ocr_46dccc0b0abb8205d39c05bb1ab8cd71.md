![](bbox=[0.158, 0.094, 0.885, 0.454])

FIGURE 18-44  Object candidateList before processing entry Lisa Fisher 2 35

We make a copy of the row corresponding to Lisa Fisher (see Figure 18-45).

![](bbox=[0.158, 0.571, 0.885, 0.692])

FIGURE 18-45  Object temp

Next, the following statement updates the voting data for region 2. (Here, region = 2 and votes = 35.)

```
temp.updateVotesByRegion(region, votes);
```

After this statement executes, the object temp is as shown in Figure 18-46.