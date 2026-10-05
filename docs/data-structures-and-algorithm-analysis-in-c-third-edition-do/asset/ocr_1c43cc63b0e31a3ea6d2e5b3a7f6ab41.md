# 17.3.2 The Halting Problem Is Unsolvable

While there might be a intellectual appeal to knowing that there exists some function that cannot be computed by a computer program, does this mean that there is any useful function? After all, does it really matter if no program can compute a “nonsense” function as shown in Bin 4 of Figure 17.7? We will now prove that the Halting Problem cannot be computed by any computer program. The proof is by contradiction.

```
boolean halt(string prog, string input) {
    if (PROGRAM_HALTS(prog, input)) {
        return true;
    else
        return false;
}
```

```
// Return the reverse of what selfhalt returns on "prog"
void contrary(char *prog) {
    if (selfhalt(prog)) {
        while (true); // Go into an infinite loop
}
```

What happens if we make a program whose sole purpose is to execute the function contrary and run that program with itself as input? One possibility is that the call to selfhalt returns true; selfhalt claims contrary will halt run on itself. In that case, contrary goes into an infinite loop (and thus does not halt). On the other hand, if selfhalt returns false, then halt is proclaiming that contrary does not halt on itself, and contrary returns,