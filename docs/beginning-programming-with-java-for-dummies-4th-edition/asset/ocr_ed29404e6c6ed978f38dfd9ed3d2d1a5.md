I waste no time in programming my computer to figure out this problem for me. When I'm finished, I have the code in Listing 7-1.

# Listing 7-1: How to Keep Four Kids from Throwing Tantrums

```
class KeepingKidsQuiet {
    public static void main(String args[]) {
        int gumballs;
        int kids;
        int gumballsPerKid;

        gumballs = 30;
        kids = 4;
        gumballsPerKid = gumballs / kids;

        System.out.print("Each kid gets ");
        System.out.print(gumballsPerKid);
        System.out.println(" gumballs.");
    }
}
```

Figure 7-1 shows a run of the KeepingKidsQuiet program. If each kid gets seven gumballs, then the kids can't complain that I'm playing favorites. They'll have to find something else to squabble about.

![](bbox=[0.12, 0.78, 0.55, 0.9])

At the core of the gumball problem, I've got whole numbers — numbers with no digits beyond the decimal point. When I divide 30 by 4, I get 7½, but I can't take the ½ seriously. No matter how hard I try, I can't divide a gumball in half, at least not without hearing "my half is bigger than his half." This fact is reflected nicely in Java. In Listing 7-1, all three variables (gumballs, kids, and gumballsPerKid) are of type int. An int value is a whole number. When you divide one int value by another (as you do with the slash in Listing 7-1), you get another int. When you divide 30 by 4, you get 7 — not 7½. You see this in Figure 7-1. Taken together, the statements

```
gumballsPerKid = gumballs/kids;
System.out.print(gumballsPerKid);
```

put the number 7 on the computer screen.