When viewed in this way, a property can consist of a setter (write-only), getter (read-only), or both (read/write). The property is never actually touched as part of the API. Here are the reasons you want to use this approach:

+   - Using a getter, it’s possible to ensure that the value supplied by the caller is the right type, the correct length, and is in a specific range. You can also verify that the data doesn’t contain viruses and other nasty stuff.
+   - Using a getter or a setter (depending on access), you can change the format of data from its internal representation to its external representation. For example, you could represent money as strings externally and floating-point values internally.
+   - Employing properties can allow you to perform security checks and other measures to keep data safe.
+   - Using getters and setters also makes it easier to set a breakpoint for debugging (discussed in Book 4 Chapter 2).
+   - Increasing property functionality can make it possible to manage resources in various ways, such as allowing access only at given times (configurable by an administrator).

Methods also access properties, but in a different manner than properties do. When designing a cash register class, you’d probably have a property representing the total dollar amount that the register contains—the methods that use the class wouldn’t directly modify that value. Instead, they’d call various methods to perform transactions. One transaction might be `Sale()`. Another transaction might be `Refund()`; another might be `Void()`. These would be the capabilities of the register in the form of public methods, and they would modify the cash value inside the register, making sure that it balances with the sales and returns. If a method could just modify the cash value directly, the balance would get out of whack. Encapsulation, then, is this:

+   - You combine the use of methods and properties to access class members, hiding some of them and making some accessible.
+   - Some methods perform specific tasks that may access more than one property.
+   - The accessible methods and properties together make up the API of the object.
+   - When you create an object, you create one that can perform on its own. In other words, the users of the class tell it what to do (such as perform a sales transaction) by calling its methods or properties and supplying parameters, and the object does the work.