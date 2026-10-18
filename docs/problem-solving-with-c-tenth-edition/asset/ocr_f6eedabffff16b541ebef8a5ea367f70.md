The variables d and w are not integers so we can’t treat them as such. For example, it would be illegal to check if (d == 0) whereas this is legal in a traditional enum. It is legal to check if (d == Days::Sun).

# 3.2 MULTIWAY BRANCHES

> "Would you tell me, please, which way I ought to go from here?"
> "That depends a good deal on where you want to get to," said the Cat.
> LEWIS CARROLL, Alice in Wonderland

Any programming construct that chooses one from a number of alternative actions is called a branching mechanism. The if-else statement chooses between two alternatives. In this section we will discuss methods for choosing from among more than two alternatives.

# Nested Statements

As you have seen, if-else statements and if statements contain smaller statements within them. Thus far we have used compound statements and simple statements such as assignment statements as these smaller substatements, but there are other possibilities. In fact, any statement at all can be used as a subpart of an if-else statement, of an if statement, of a while statement, or of a do-while statement. This is illustrated in Display 3.3. The statement in that display has three levels of nesting, as indicated by the boxes. Two cout statements are nested within an if-else statement, and that if-else statement is nested within an if statement.

When nesting statements, you normally indent each level of nested substatements. In Display 3.3 there are three levels of nesting, so there are three levels of indenting. Both cout statements are indented the same amount

# DISPLAY 3.3 An if-else Statement Within an if Statement

```
1  if (count > 0)
2    if (score > 5)
3      cout << "count > 0 and score > 5\n";
4    else
5      cout << "count > 0 and score <= 5\n";
```