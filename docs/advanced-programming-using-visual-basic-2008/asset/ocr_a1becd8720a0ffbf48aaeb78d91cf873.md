# Summary Form

Display the total number and the total dollar amounts for deposits, checks, interest, and service charges.

# Business Services Tier

Validate that the balance can cover a check. If not, throw an exception and deduct a service charge of $10; do not process the check. Process interest and deposits by adding to the balance and checks and service charges by reducing the balance.

# Optional Extra

Create an MDI application that includes an About form, a toolbar, and a status bar.

# 2.4

Piecework workers are paid by the piece. Workers who produce a greater quantity of output are often paid at a higher rate.

# Presentation Tier

The program should input the name and number of pieces and calculate the pay. Include a *Calculate* button and a *Clear* button. You can include either a *Summary* form or menu item. The *Summary* option displays the total number of pieces, the total pay, and the average pay per person on a Summary form.

The name and number of pieces are required fields.

# Business Services Tier

The number of pieces must be a positive number; throw an exception for negative numbers. Calculate the pay using this schedule:

| Pieces completed | Price paid per piece for all pieces |
|---|---:|
| 1–199 | .50 |
| 200–399 | .55 |
| 400–599 | .60 |
| 600 or more | .65 |

Accumulate and return the summary totals for number of pieces, pay, and average pay per person. Notice that you also must accumulate the number of persons to calculate the average.

# 2.5

Add an inherited class to Exercise 2.4. This class calculates pay for senior workers, who are paid on a different scale. You must add a check box to the form for senior workers and use the inherited class for those workers.

Senior workers receive a base pay of $300 plus a per-piece pay using this schedule:

| Pieces completed | Price paid per piece for all pieces |
|---|---:|
| 1–199 | .20 |
| 200–399 | .25 |
| 400–599 | .30 |
| 600–799 | .35 |
| 800 or more | .40 |