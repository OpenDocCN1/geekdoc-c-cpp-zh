The initial and final states indicate the **single entry point** and the **single exit point** of each control statement. Arbitrarily connecting individual symbols in an activity diagram can lead to unstructured programs. Therefore, the programming profession has chosen a limited set of control statements that can be combined in only two simple ways to build structured programs.

For simplicity, C++ includes only **single-entry/single-exit** control statements—there's only one way to enter and only one way to exit each control statement. Connecting control statements in sequence to form structured programs is simple. The final state of one control statement is connected to the initial state of the next—that is, the control statements are placed in a program one after another in sequence. We call this control-statement stacking. The rules for forming structured programs also allow for **nested control statements**.

# Rules for Forming Structured Programs

Figure 4.12 shows the rules for forming structured programs. The rules assume that action states may be used to indicate *any* action. The rules also assume that we begin with the simplest activity diagram (Fig. 4.13) consisting of only an initial state, an action state, a final state and transition arrows.

+   **Rules for forming structured programs**
+   
+   1. Begin with the simplest activity diagram (Fig. 4.13).
+   2. Any action state can be replaced by two action states in sequence.
+   3. Any action state can be replaced by any control statement (sequence of action states, if, if…else, switch, while, do…while or for).
+   4. Rules 2 and 3 can be applied as often as you like and in any order.

**Fig. 4.12** | Rules for forming structured programs.

![](bbox=[0.44, 0.58, 0.56, 0.74])

**Fig. 4.13** | Simplest activity diagram.