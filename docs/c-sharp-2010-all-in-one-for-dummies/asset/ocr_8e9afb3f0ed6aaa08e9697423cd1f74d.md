# # Chapter 7: Poly-what-ism?

# ## In This Chapter

+   - Deciding whether to hide or override a base class method (so many choices!)
+   - Building abstract classes — are you for real?
+   - Declaring a method and the class that contains it to be abstract
+   - Using ToString, the class business card
+   - Sealing a class from being subclassed

In inheritance, one class "adopts" the members of another. Thus I can create a class SavingsAccount that inherits data members such as account_id and methods such as Deposit() from a base class BankAccount. That's useful, but this definition of inheritance isn't sufficient to mimic what's going on out there in the business world.

> > TIP: See Chapter 6 of this minibook if you don't know (or remember) much about class inheritance.

A microwave oven is a type of oven, not because it looks like an oven but, rather, because it performs the same functions as an oven. A microwave oven may perform additional functions, but it performs, at the least, the base oven functions — most importantly, heating up my nachos when I say, "StartCooking." (I rely on my object of class Refrigerator to cool the beer.) I don't particularly care what the oven must do internally to make that happen, any more than I care what type of oven it is, who made it, or whether it was on sale when my wife bought it. (Hey, wait — I do care about that last one.)

From our human vantage point, the relationship between a microwave oven and a conventional oven doesn't seem like such a big deal, but consider the problem from the oven's point of view. The steps that a conventional oven performs internally are completely different from those that a microwave oven may take.

> > REMEMBER: The power of inheritance lies in the fact that a subclass doesn't have to inherit every single method from the base class just the way it's written. A subclass can inherit the essence of the base class method while implementing the details differently.