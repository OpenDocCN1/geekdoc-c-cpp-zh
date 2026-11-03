by top is set to 3.9. The final assignment does nothing but waste time since top points at first_point.

Structure and union references are not changed to pointers, as are array and function references, when they appear where a scalar is required in an expression. Hence, about all that you can do with a structure or union is select one of its parts or take its address. The following example shows how to use unions in a safe way:

```
struct card_variant {char vtag; char rank, suit;};
struct joker_variant {char vtag; int num;};
union {struct card_variant card;
struct joker_variant joker;} deck[54];
/* initialize the deck of 52 cards & 2 jokers */
if (deck[k].card.vtag == 'C')
{if (deck[k].card.suit == 'H') ...etc.}
else if (deck[k].card.vtag == 'J')
{if (deck[k].joker.num < 3) ...etc.}
else
{error ("bad card");}
```

# 3.6 Function calls

The functions of C are invoked by function calls of the following form:

```
function-name-expr ( expr-list )_opt
```

where function-name-expr has the syntax rule

```
function-name-expr =
{ function-name
| (* function-pointer-expr )
}
```

The function-name-exprs range in complexity from simple names like sqrt to complicated ones like (*p -> clk - 2l.pfch) which means that the function pointed to by the pointer part pfch of the (k - 2)-th item in array part c of the structure pointed to by pointer variable p. The parts focussing operators -> and . have the highest precedence (along with [] and ()), so the dereferencing operator * is the last one applied in the above expres-