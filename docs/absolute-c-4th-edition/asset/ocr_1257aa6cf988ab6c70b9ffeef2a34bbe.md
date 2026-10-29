# Display 3.8  **Local Variables (part 2 of 2)**

# SAMPLE DIALOGUE

```
Enter minimum and maximum number of peas in a pod: 4 6
Enter the number of pods: 10
Enter the weight of an average pea (in ounces): 0.5
Min number of peas per pod = 4
Max number of peas per pod = 6
Pod count = 10
Average pea weight = 0.500 ounces
Estimated average yield = 25.000 ounces
```

When the variable averagePea is given a value in the function call to estimateOfTotal, this does not change the value of the variable in the main function that is also named averagePea.

Variables that are declared within the body of a function definition are said to be **local** to that function or to have that function as their **scope**. If a variable is local to some function, you sometimes simply call it a local variable, without specifying the function.

Another example of local variables can be seen in Display 3.5. The definition of the function totalCost in that program begins as follows:

```
double totalCost(int numberParameter, double priceParameter)
{
    const double TAXRATE = 0.05; //5% sales tax
    double subtotal;
```

The variable subtotal is local to the function totalCost. The named constant TAXRATE is also local to the function totalCost. (A named constant is in fact nothing but a variable that is initialized to a value and that cannot have that value changed.)

# LOCAL VARIABLES

Variables that are declared within the body of a function definition are said to be local to that function or to have that function as their scope. If a variable is local to a function, then you can have another variable (or other kind of item) with the same name that is declared in another function definition; these will be two different variables, even though they have the same name. (In particular, this is true even if one of the functions is the main function.)