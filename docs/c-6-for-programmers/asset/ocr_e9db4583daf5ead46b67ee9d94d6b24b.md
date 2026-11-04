where the *initialization* expression names the loop’s control variable and provides its initial value, the *loopContinuationCondition* determines whether looping should continue and the *increment* modifies the control variable’s value (whether an increment or decrement), so that the loop-continuation condition eventually becomes false. The two semicolons in the *for* header are required. We don’t include a semicolon after *statement*, because the semicolon is already assumed to be included in the notion of a *statement*.

# ### 6.3.3 Scope of a *for* Statement’s Control Variable

If the *initialization* expression in the *for* header declares the control variable (i.e., the control variable’s type is specified before the variable name, as in Fig. 6.2), the control variable can be used *only* in that *for* statement—it will not exist outside it. This restricted use of the name of the control variable is known as the variable’s *scope*. The scope of a variable defines where it can be used in an app. For example, a local variable can be used only in the method that declares the variable and *only* from the point of declaration through the end of the block in which the variable has been declared. Scope is discussed in detail in Chapter 7, *Methods: A Deeper Look*.

**Common Programming Error 6.1**

When a *for* statement’s control variable is declared in the initialization section of a *for*’s header, using the control variable after the *for*’s body is a compilation error.

# ### 6.3.4 Expressions in a *for* Statement’s Header Are Optional

All three expressions in a *for* header are optional. If the *loopContinuationCondition* is omitted, C# assumes that it’s *always true*, thus creating an *infinite loop*. You can omit the *initialization* expression if the app initializes the control variable *before* the loop—in this case, the scope of the control variable will *not* be limited to the loop. You can omit the *increment* expression if the app calculates the increment with statements in the loop’s body or if no increment is needed. The *increment* expression in a *for* acts as if it were a standalone statement at the end of the *for*’s body. Therefore, the expressions

```
    counter = counter + 1
    counter += 1
    ++counter
    counter++
```

are equivalent increment expressions in a *for* statement. Many programmers prefer counter++ because it’s concise and because a *for* loop evaluates its increment expression *after* its body executes—so the postfix increment form seems more natural. In this case, the variable being incremented does not appear in a larger expression, so the prefix and postfix increment operators have the *same* effect.

# ### 6.3.5 UML Activity Diagram for the *for* Statement

Figure 6.4 shows the activity diagram of the *for* statement in Fig. 6.2. The diagram makes it clear that initialization occurs only once—*before* the loop-continuation test is evaluated the first time—and that incrementing occurs *each* time through the loop *after* the body statement executes.