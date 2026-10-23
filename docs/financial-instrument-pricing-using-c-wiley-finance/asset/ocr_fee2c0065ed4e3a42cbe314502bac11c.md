in applications and access the elements in lattices. To this end, we create generic code in Layer 2 that realises these features. In the past (Duffy, 2006A) we used an object-oriented approach that led to code that was somewhat inflexible and that introduced coupling into the framework. With the advent of C++11 we now have the opportunity to improve the genericity and maintainability of the framework. In this chapter we discuss the following features:

+   - Tuples that we use as return types of functions or as input arguments to functions.
+   - The function type wrapper `std::function<>`. This is a *signature-based feature* and it reduces the coupling between components because it is a specification and its implementations have been postponed to code in Layer 3. We have already seen in Chapters 3 and 4 that function type wrappers can be implemented as *callable objects* such as free functions, static member functions, object member functions (in combination with `std::bind<>`), function objects and lambda functions.
+   - Lambda functions that are used in Layer 3 of the framework.
+   - Using the keyword `auto` for automatic type deduction. This feature helps to make the code more readable and it takes the drudgery out of programming.

We also remark that it is possible to create function wrappers whose input arguments and return type are tuples. It is also possible to create tuples whose elements are function wrappers.

Having created a lattice, we then discuss algorithms that use or modify its elements. In order to reduce the scope, we focus on the well-known *forward* and *backward induction algorithms* (see Clewlow and Strickland, 1998; Duffy, 2006A; Duffy and Germani, 2013). In general, we access and modify binomial and trinomial lattices in different ways, for example:

+   - U1: Forward induction (create the lattice using *up* and *down* parameters).
+   - U2: Compute the payoff at each final node (maturity/expiration).
+   - U3: Backward induction (compute the option value at earlier nodes starting from expiration).

Some other use cases are:

+   - U4: Computing hedge sensitivities.
+   - U5: Lattice models for dividend-paying assets.
+   - U6: Pricing path-dependent options.
+   - U7: Computing the price of American put options.
+   - U8: Two-factor lattice methods.

To this end, we have created four free functions to realise forward and backward induction, one set of functions for plain options and another set for American options. We also make a distinction between binomial and trinomial lattices. There are opportunities to make the code more elegant. We also make use of function wrappers and tuples.