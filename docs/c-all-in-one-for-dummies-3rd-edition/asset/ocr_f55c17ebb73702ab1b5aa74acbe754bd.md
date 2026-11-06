Now look at Figure 3-2. Here, you have a diamond and a line, which again mean composition. But this time the Porsche class has a 1 by it, and the GoodyearTire class has a 4 by it. This combination means that exactly one instance of Porsche will have exactly four instances of GoodyearTire. In other words, one car has four tires.

**Figure 3-2:** The diamond and the line combined mean composition.

![](bbox=[0.234, 0.255, 0.608, 0.359])

Next, look at Figure 3-3. Again, you see an association, but this time it is between the Pasture class and the Cow class. But in this case, the Pasture class has a 1 by it, and the Cow class has an asterisk (*) by it. The asterisk indicates that any number of Cow instances can be associated with any single Pasture instance. In other words, a single pasture can have multiple cows running around on it. When you put an asterisk in the UML diagram, it indicates that any number of instances can be in the association, including 0. Therefore, a Pasture might have no cows in it (they’re all in the barn being milked), or just 1 might be in the pasture, or 100 cows may be out in the pasture, lounging around.

**Figure 3-3:** Many instances of the class with the * nearby can be associated with the class with the 1 nearby.

![](bbox=[0.234, 0.63, 0.608, 0.724])

Other possibilities for denoting the number of items in a relationship are also available. These possibilities are called *multiplicities*. Table 3-1 lists them.