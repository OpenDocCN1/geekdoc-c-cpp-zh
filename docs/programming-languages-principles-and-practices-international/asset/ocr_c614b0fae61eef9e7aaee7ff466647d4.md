an activation record that no longer exists. Any subsequent call to that procedure will have an incorrect access environment.

Consider the following example, in which we may reasonably want a procedure to create another procedure. We write this example in Ada95, since Ada95 has procedure types and parameters, and so can express the situation quite well (this example is adapted from Abelson and Sussman [1996]):

```
type WithdrawProc is
    access function (x: integer) return integer;

InsufficientFunds: exception;

function makeNewBalance (initBalance: integer)
    return WithdrawProc
is
    currentBalance: integer;

    function withdraw (amt: integer) return integer is
    begin
        if amt <= currentBalance then
            currentBalance := currentBalance - amt;
        else
            raise InsufficientFunds;
        end if;
        return currentBalance;
    end withdraw;

begin
    currentBalance := initBalance;
    return withdraw'access;
end makeNewBalance;
```

We now might want to make two different accounts from which to withdraw, one with an initial balance of 500 and the other with an initial balance of 100 dollars:

```
withdraw1, withdraw2: WithdrawProc;

withdraw1 := makeNewBalance(500);
withdraw2 := makeNewBalance(100);
```

The problem is that in a stack-based environment, the activation records in which both these functions were created have disappeared: Each time makeNewBalance returns, the local environment of makeNewBalance is released. For example,

```
newBalance1 := withdraw1(100);
newBalance2 := withdraw2(50);
```