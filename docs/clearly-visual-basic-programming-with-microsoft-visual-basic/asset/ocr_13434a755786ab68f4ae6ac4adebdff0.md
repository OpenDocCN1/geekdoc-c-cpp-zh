Figure 16-7 shows the planning information for the modified Monthly Payment Calculator application. The algorithm will display the monthly payments by rate within term.

```
Output:     monthly payment (for each annual interest rate within each term)
Processing: annual interest rate (counter that counts from 4% through 7% in increments of 1%)
            term (counter that counts from 2 years through 5 years in increments of 1 year)
Input:      principal

Algorithm:
1. enter the principal
2. remove any previous monthly payments from the Payments box
3. repeat for terms from 2 years through 5 years in increments of 1 year
    display the term in the Payments box
    repeat for annual interest rates from 4% through 7% in increments of 1%
        calculate the current monthly payment using the principal, term, and current
        annual interest rate
        display the current annual interest rate and the current monthly payment in the
        Payments box
    end repeat
    display a blank line in the Payments box to separate the current term's information from
    the next term's information
end repeat
```

Figure 16-7: Planning information for the modified Monthly Payment Calculator application

# **To open the Monthly Payment Calculator application, and then code the application:**

+   1. Open the **Monthly Payment Solution (Monthly Payment Solution.sln)** file, which is contained in the ClearlyVB\Chap16\Monthly Payment Solution-Version 1 folder. If necessary, open the designer window. The application’s user interface is shown in Figure 16-8. The user will enter the principal in the txtPrincipal control. When the user clicks the Calculate Monthly Payments button, the payments will appear in the txtPayments control.