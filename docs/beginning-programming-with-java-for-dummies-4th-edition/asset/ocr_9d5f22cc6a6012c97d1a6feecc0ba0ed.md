# Barry makes good on an age-old promise

In Chapter 6, I pull a variable declaration outside of a main method. I go from code of the kind in Listing 18-9 to code of the kind that's in Listing 18-10.

# Listing 18-9: Declaring a Variable Inside the main Method

```
class SnitSoft {
    public static void main(String args[]) {
        double amount = 5.95;
        amount = amount + 25.00;
        System.out.println(amount);
    }
}
```

# Listing 18-10: Pulling a Variable Outside of the main Method

```
class SnitSoft {
    static double amount = 5.95;
    public static void main(String args[]) {
        amount = amount + 25.00;
        System.out.println(amount);
    }
}
```

In Chapter 6, I promise to explain why Listing 18-10 needs the extra word static (in static double amount = 5.95). Well, with all the fuss about static methods in this chapter, I can finally explain everything.

Refer to Figure 18-7. In that figure, you have checks, and you have a sort method. Each individual check has its own number, its own amount, and its own payee. But the entire Check class has just one sort method.

I don't know about you, but to sort my cancelled checks, I hang them on my exotic Yucca Elephantipes tree. I fasten the higher numbered checks to the upper leaves and put the lower numbered checks on the lower leaves. When I find a check whose number comes between two other checks, I select a free leaf (one that's between the upper and lower leaves).