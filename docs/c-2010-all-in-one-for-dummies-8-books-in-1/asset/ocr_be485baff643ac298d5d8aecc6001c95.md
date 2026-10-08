# 316 Polymorphism

The second question is subtle. When passed a BankAccount object, MakeAWithdrawal() invokes BankAccount.Withdraw() — that clear enough. But when passed a SavingsAccount object, MakeAWithdrawal() calls the same method. Shouldn't it invoke the Withdraw() method in the subclass?

The prosecution intends to show that the call ba.Withdraw() should invoke the method BankAccount.Withdraw(). Clearly, the ba object is a BankAccount. To do anything else would merely confuse the state. The defense has witnessed in Main (to prove that the ba object is declared BankAccount, and it in fact a SavingsAccount. The delocked arguments are equally valid.

In this case C# comes down on the side of the prosecution. The safer of the two possibilities is to go with the declared type because it avoids any miscommunication. The object is declared to be a BankAccount and that's that. However, that may not be what you want.

# Using the declared type every time
(Is that so wrong?)

In some cases, you don't want to choose the declared type. What you want (or, "what you really, really want," to quote the popular Spice Girls song) is to make the call based on the real type — the runtime type — as opposed to the declared type. For example, you want to use the SavingsAccount stored in a BankAccount variable. This capability to decide at runtime is known as polymorphism, or late binding. Using the declared type every time is early binding because it sounds like the opposite of late binding.

![](bbox=[0.123, 0.606, 0.215, 0.663])

The ridiculous term polymorphism comes from the Greek language: Poly means "more than one," morph means "transform," and ism a fairly useless term. But we're stuck with it.

Polymorphism and late binding aren't exactly the same concept — but the difference is:

+   * Polymorphism refers to the general ability to decide which method to invoke at runtime.
* Late binding refers to the specific way a language implements polymorphism.

Polymorphism is the key to the power of object-oriented (OO) programming. It's so important that languages that don't support it can't advertise them-as OO languages. (If I think it's an FDA regulation: you can't label a