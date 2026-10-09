single stock price and a fixed interest rate *r*. This will be sufficient to highlight the key ideas, but obviously would need to be revisited if one was writing a real trading system.

By making **ContinuousTimeOption** extend **Priceable**, we can ensure that all our options classes implement **Priceable**. We will leave writing additional classes **Stock** and **ZeroCouponBond** as exercises for the reader (see Exercise 13.5.1 for the definition of a zero-coupon bond).

# 13.2 The Portfoli o interface and implementation

Now that we have designed our **Priceable** class it is easy to design the key functions of a **Portfoli o**. A **Portfoli o** class must have the following key functions:

+   (i) a function to add a **Priceable** instance together with an associated quantity;

+   (ii) a function to change the quantity held of a given security;

+   (iii) a function **price** to compute the value of the **Portfoli o**.

The last item suggests that a **Portfoli o** should itself implement the interface **Priceable**. This means that it will be possible to create a **Portfoli o** that itself contains **Portfoli os**. This accurately reflects how banks manage their books. They organise their holdings into a number of different portfolios first by line of business, then by trading desk, then by trader. Each trader will then maintain a number of separate portfolios simply as a means of organising their work.

One can see that our **Portfoli o** implementation will need some way to store objects of type **Priceable** in order to keep track of the investor’s position. It not possible for the **Portfoli o** implementation to have member variables of type **Priceable** because **Priceable** is an abstract class. For the same reason it is impossible to have a vector of **Priceable** objects. The fundamental reason for this is that member variables and elements of vectors must all be of the same size. Different **Priceable** objects will take up different amounts of memory depending upon the variables they contain.

The solution for this is for the **Portfoli o** to store data using **shared_ptr**. This unavoidable use of pointers was the reason we had to introduce the topic of pointers in Chapter 11.

This leads us to the following decisions about the design for the **Portfoli o** class.

+   (i) Our **Portfoli o** implementation will hold a vector of **shared_ptr** objects that point to **Priceable** instances.