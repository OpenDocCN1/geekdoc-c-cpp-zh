4.8 What does it mean to say an object is default initialized? Default initialization is never considered ineffective even if the object is later re-initialized. Why not?

4.9 Consider the following simple package with a global variable and a swap procedure that exchanges its parameter with the global variable:

```
package Example is
  G : Integer;

  procedure Swap(X : in out Integer)
    with Global => (In_Out => G);
  end Example;
```

What flow dependency contract is synthesized for Swap? Is it accurate?

4.10 When a contract is synthesized, it is not checked in the body of the subprogram to which the contract applies. Consider the following subprogram with a flow dependency contract:

```
procedure P(X : in out Integer)
  with Depends => (X =>+ A, A => B);
```

+   a. What data dependency contract is synthesized?
+   b. If P's body, in fact, makes use of another global variable C, will the inconsistency be detected? Be careful!

4.11 When a contract is synthesized, it is not checked in the body of the subprogram to which the contract applies. Consider the following subprogram with a data dependency contract:

```
procedure P(X : in out Integer)
  with Global => (Input => A, Output => B);
```

+   a. What flow dependency contract is synthesized?
+   b. If P's body does not actually have one of the flow dependencies in the synthesized contract, will the inconsistency be detected?

4.12 We recommend explicitly declaring data and flow dependency contracts on the public subprograms of a package. Why?

4.13 When is it reasonable to rely on synthesized data and flow dependency contracts?

4.14 What is the difference between constructive analysis and retrospective analysis?