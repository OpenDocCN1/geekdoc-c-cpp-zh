# Polymorphic Public Inheritance 723

+   - Withdrawing money from the account
- Displaying the account information

For the Brass Plus Account checking plan, the Pontoon National Bank wants all the features of the Brass Account as well as the following additional items of information:

+   - An upper limit to the overdraft protection
- An interest rate charged for overdraft loans
- The overdraft amount currently owed to the bank

No additional operations are needed, but two operations need to be implemented differently:

+   - The withdrawing money operation has to incorporate overdraft protection for the Brass Plus Account
- The display operation has to show the additional information required by the Brass Plus Account

Suppose you call one class Brass and the second class BrassPlus. Should you derive BrassPlus publicly from Brass? To answer this question, first answer: Does the BrassPlus class meet the is-a test? Everything that is a Brass object will be true for a BrassPlus object. Store a client name, an account number, and a balance. With both, you can make deposits and withdrawals and display account information. Note that the is-a relationship is not, in general, symmetric. A fruit, in general, is not a banana; similarly, a Brass object won't have all the capabilities of a BrassPlus object.

# Developing the Brass and BrassPlus Classes

The Brass Account class information is pretty straightforward, but the bank hasn't told you enough details about how the overdraft system works. In response to your request for further information, the friendly Pontoon National Bank representative tells you the following:

+   - A Brass Plus Account limits how much money the bank will lend you to cover overdrafts. The default value is $500, but some customers may start with a different limit.
- The bank may change a customer's overdraft limit.
- A Brass Plus Account charges interest on the loan. The default value is 11.125%, but some customers may start with a different rate.
- The bank may change a customer's interest rate.
- The account keeps track of how much the customer owes the bank (overdraft loans plus interest). The user cannot pay off this amount through a regular deposit