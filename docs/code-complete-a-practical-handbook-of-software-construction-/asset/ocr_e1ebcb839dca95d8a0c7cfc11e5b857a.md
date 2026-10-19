In other words, all the routines defined in the base class should mean the same thing when they’re used in each of the derived classes.

If you have a base class of *Account* and derived classes of *CheckingAccount*, *SavingsAccount*, and *AutoLoanAccount*, a programmer should be able to invoke any of the routines derived from *Account* on any of *Account*’s subtypes without caring about which subtype a specific account object is.

If a program has been written so that the Liskov Substitution Principle is true, inheritance is a powerful tool for reducing complexity because a programmer can focus on the generic attributes of an object without worrying about the details. If a programmer must be constantly thinking about semantic differences in subclass implementations, then inheritance is increasing complexity rather than reducing it. Suppose a programmer has to think this: “If I call the *InterestRate()* routine on *CheckingAccount* or *SavingsAccount*, it returns the interest the bank pays, but if I call *InterestRate()* on *AutoLoanAccount* I have to change the sign because it returns the interest the consumer pays to the bank.” According to LSP, *AutoLoanAccount* should not inherit from the *Account* base class in this example because the semantics of the *InterestRate()* routine are not the same as the semantics of the base class’s *InterestRate()* routine.

**Be sure to inherit only what you want to inherit** A derived class can inherit member routine interfaces, implementations, or both. Table 6-1 shows the variations of how routines can be implemented and overridden.

**Table 6-1 — Variations on Inherited Routines**

|  | Overridable | Not Overridable |
|---|---|---|
| **Implementation: Default Provided** | Overridable Routine | Non-Overridable Routine |
| **Implementation: No Default Provided** | Abstract Overridable Routine | Not used (doesn’t make sense to leave a routine undefined and not allow it to be overridden) |

As the table suggests, inherited routines come in three basic flavors:

+   - An *abstract overridable routine* means that the derived class inherits the routine’s interface but not its implementation.
+   - An *overridable routine* means that the derived class inherits the routine’s interface and a default implementation and it is allowed to override the default implementation.
+   - A *non-overridable routine* means that the derived class inherits the routine’s interface and its default implementation and it is not allowed to override the routine’s implementation.