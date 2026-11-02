information just as a traditional Ada compiler checks the consistency of each call’s arguments.

There are many implementations of Search that will satisfy the parameter types and modes. A large number of those implementations have nothing to do with searching a string for a particular character, despite whatever suggestive names are used. The flow dependency contract rules out some of those implementations as flow errors leaving behind a smaller set of implementations that conform to both the parameter types and modes and the flow dependency contract.

However, it is still easy to see that many incorrect implementations of Search exist that satisfy the flow dependency contract. To further tighten the possibilities, the programmer can use pre- and postconditions to describe more precisely the relationship between the subprogram’s outputs and its inputs. We introduced the Pre and Post aspects with the bounded queue package in Section 3.3. We cover these aspects in more detail in Section 6.2.

One important point, however, is that flow dependency contracts must be complete. If you use the Depends aspect at all, you must fully describe all flows into and out of the subprogram, including flows involving global data described by the data dependency contract. In contrast, as you will see, pre- and postconditions are often incomplete. They may not describe every aspect of the relationship between inputs and outputs. In this respect effective use of pre- and postconditions depends significantly on your skill with them and on the proof technology being used. However, flow contracts are more reliable in the sense that your program will simply not pass SPARK examination until it is completely free of flow errors.

# ### 4.2.1 Flow Dependency Contract Abbreviations

In general, a flow dependency contract consists of an association between each output of a subprogram and a list of the inputs on which that output depends. Writing these associations can be tedious and repetitive so SPARK provides two important abbreviations that make writing flow dependency contracts easier.

First, it is common for multiple outputs to depend on the same inputs. An especially common case, although not universal, is when each output depends on all inputs. The procedure Search shown previously is like this. The syntax of flow dependency contracts allows the programmer to associate a list of outputs with a list of inputs. Thus, a contract such as

```
```
with
   Depends => (Found => (Text, Letter, Start),
               Position => (Text, Letter, Start))
```
```