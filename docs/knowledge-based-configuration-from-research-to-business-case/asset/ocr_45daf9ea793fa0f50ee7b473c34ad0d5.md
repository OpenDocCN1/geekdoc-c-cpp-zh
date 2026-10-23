```
1.  kbase GPRS Cell;
2.  component P2PMeter {
3.    attribute int mdist,codeset,mRate;
4.    constraints {
5.      mdist = {1..3};
6.      codeset = {1..4};
7.    }
8.  }
9.  component FPC {
10. attribute int value;
11. constraints(default){
12.   value = 1;
13. }
14. constraints(x1){
15.   value = {2..4};
16. }
17. constraints(unknown){
18.
19. }
20. }
21. component BTS {
22.   attribute int fpc;
23.   constraints{
24.     FPC fpc1;
25.     fpc = fpc1.value;
26.   }
27. }
28. component Cell {
29.   attribute int neededR, realR;
30.   constraints {
31.     BTS b1;
32.     P2PMeter s[100];
33.     realR=sum([s], mRate)/P2PNo;
34.     realR>=neededR;
35.    ...//neededR is internally computed
36.   }
37.   transition {
38.     forall ( P2PMeter ) {
39.       if (mdist=1 and codeset = 2 )
40.         codeset.next = {2,3}
41.       if (mdist=3 and codeset = 2 )
42.         codeset.next = {2,1};
43.     }
44.   }
45. }
```

# FIGURE 19.4

A SIMOL program. For reasons of space limitations, we omitted the attributes dbr, dlpr, doa, iptlogin, etc. in Line 3, their initialization in the constraints section of the Cell component, and also the definition of the ATS component from Figure 19.3.

requirements, COMP is a set of attributes that can be changed, and MODES represents the set of all functional modes defined for the elements in COMP.

This definition is almost equivalent to the definition of the diagnosis problem accordingly to (Reiter (1987)) and indeed the relationship between diagnosis and reconfiguration has been already pointed out (e.g., Crow and Rushby, 1991; Provan and Chen, 1999; Stumptner and Wotawa, 1998). Unlike Crow and Rushby (1991) and Provan and Chen (1999), we do not interleave diagnosis and reconfiguration in our approach (the constraint solver determines reconfigurations directly, i.e., without using any previously computed diagnoses). The slight difference to Stumptner and Wotawa (1998) is that in this work we rely purely on consistency-based reasoning ignoring fault models, which is sufficient for our purpose.

As we have already seen, SIMOL can be used to describe SD, REQ, COMP, and MODES. The assignment of attributes/components (COMP) to functional modes (MODES) can be defined as follows.

Definition (Mode assignment). Given the set of configurable attributes COMP and the set of all functional modes MODES. A mode assignment M is a function M : COMP → MODES mapping each component to one of its modes.

A solution to the reconfiguration problem can be easily formalized using the definition of diagnosis introduced by Reiter (1987).