| Nouns and noun phrases in the requirements specification |
| bank | money / fund | account number |
| ATM | screen | PIN |
| user | keypad | bank database |
| customer | cash dispenser | balance inquiry |
| transaction | $20 bill / cash | withdrawal |
| account | deposit slot | deposit |
| balance | deposit envelope |  |

Fig. 3.18 | Nouns and noun phrases in the requirements specification.

maintains a count of the number of bills it contains. The requirements specification doesn’t say anything about what the system should do with deposit envelopes after it receives them. We can assume that acknowledging the receipt of an envelope—an operation performed by the class that models the deposit slot—is sufficient to represent the presence of an envelope in the system. (We assign operations to classes in Section 6.22.)

In our simplified ATM system, representing various amounts of “money,” including the “balance” of an account, as attributes of other classes seems most appropriate. Likewise, the nouns “account number” and “PIN” represent significant pieces of information in the ATM system. They are important attributes of a bank account. They do not, however, exhibit behaviors. Thus, we can most appropriately model them as attributes of an account class.

Though the requirements specification frequently describes a “transaction” in a general sense, we do not model the broad notion of a financial transaction at this time. Instead, we model the three types of transactions (i.e., “balance inquiry,” “withdrawal” and “deposit”) as individual classes. These classes possess specific attributes needed for executing the transactions they represent. For example, a withdrawal needs to know the amount of money the user wants to withdraw. A balance inquiry, however, does not require any additional data. Furthermore, the three transaction classes exhibit unique behaviors. A withdrawal includes dispensing cash to the user, whereas a deposit involves receiving deposit envelopes from the user. [Note: In Section 13.10, we “factor out” common features of all transactions into a general “transaction” class using the object-oriented concepts of abstract classes and inheritance.]

We determine the classes for our system based on the remaining nouns and noun phrases from Fig. 3.18. Each of these refers to one or more of the following:

+   - ATM
+   - screen
+   - keypad
+   - cash dispenser
+   - deposit slot
+   - account
+   - bank database
+   - balance inquiry
+   - withdrawal
+   - deposit

The elements of this list are likely to be classes we’ll need to implement our system.