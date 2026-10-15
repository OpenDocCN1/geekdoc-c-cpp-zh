the method returned, that formal parameter was destroyed and the Num object it referred to was marked for garbage collection. The only change that is “permanent” is the change made to the state of the second parameter. Figure 7.5 shows the step-by-step processing of this program.

# STEP 1

Before invoking changeValues

# STEP 2

```
tester.changeValues (a1, a2, a3);
```

# STEP 3

```
f1 = 999;
```

# STEP 4

```
f2.setValue (888);
```

# STEP 5

```
f3 = new Num (777);
```

# STEP 6

After returning from changeValues

□ = Undefined

# FIGURE 7.5 Tracing the parameters in the ParameterTesting program