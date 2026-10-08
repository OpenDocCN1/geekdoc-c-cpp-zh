# CHAPTER 6

# More on the Selection Structure

| Correct algorithm | Incorrect algorithm |
|---|---|
| 1. enter the code and sales | 1. enter the code and sales |
| 2. calculate the bonus by multiplying | 2. calculate the bonus by multiplying |
| the sales by .08 | the sales by .08 |
| 3. if (the code is X) | 3. (if the code is X and the sales are greater |
| if (the sales are greater than | than or equal to 10000) |
| equal to 10000) | add 150 to the bonus |
| else | else |
| add 150 to the bonus | add 125 to the bonus |
| else | end if |
| add 125 to the bonus | 4. display the bonus |
| end if |
| 4. display the bonus |

176

Figure 16 Correct algorithm and an incorrect algorithm contains the first logic error

To understand why the incorrect algorithm in Figure 6-15 will not work cor- rectly, you will de-check using the same test data used to de-check the correct algorithm. The first instruction in the incorrect algorithm is to enter the code and sales. For the first-check, the code and sales are X and 15000, respectively. The second instruction is to calculate the bonus by multiplying the sales by .08; the answer is 1200. The condition in the third instruction determines whether the salesperson's code is X, and at the same time, the sales are greater than or equal to 10000. In this case, the selection structure's true path adds 150 to the bonus, 1350, and then the selection structure ends. The last instruction in the incorrect algorithm displays the bonus (1350) on the screen. Even though its selection is phrased incorrectly, the incorrect algorithm produces the same result as the correct algorithm using the first set of test data.

Using the second set of test data, the user enters X as the code and 9000 as the sales. The second instruction in the incorrect algorithm multiplies the sales by .08, giving a bonus of 720. The condition in the third instruction determines the salesperson's code is X, and at the same time, the sales are greater than or equal to 10000. In this case, the compound evaluates to fail, because the sales do not meet the specified criteria. As result, the selection structure's false path adds 125 to the bonus, giving 845, and then the selection structure ends. The last instruction in the incorrect algorithm displays the bonus (845) on the screen. Here, using the second set of test data, the incorrect algorithm produces the result as the correct algorithm.

Using the third set of test data, the user enters A as the code and 13000 as the sales. The second instruction in the incorrect algorithm multiplies the sales by .08, giving a bonus of 1040. The condition in the third instruction determines whether the salesperson's code is X, and at the same time, the sales are greater than or equal to 10000. In this case, the compound evaluates to fail, because the salesperson's code is not X. As result, the selection structure' false path adds 125 to the bonus, giving 1165, and then the selection structure ends. The last instruction in the incorrect algorithm displays the bonus (1165) on the screen. Notice that the incorrect algorithm produces erroneous results using the third set of test data: According to Figure 6-10, the