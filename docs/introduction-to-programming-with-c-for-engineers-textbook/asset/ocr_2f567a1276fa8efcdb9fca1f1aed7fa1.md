# Listing 6.30 (continued)

```
ExpressionTreeBuilderInterpreter exprParser;
string good_expr( "(1+2)*(3+(4+5))/(6-7)" );

// Let's call only the base class operator ()
if( exprParser.BaseClass::operator()( good_expr ) )
{
```

To make our exprParser - defined on line [11] as an object of the Expression TreeBuilderInterpreter class - perform parsing without any final postprocessing of the syntax tree, line [16] invokes operator() from the base class. To accomplish this, we have to put the name of the base class before the name exprParser of the object and the name of the member function. In our case, the name of the base class is TSimpleExpressionInterpreter, for which an alias BaseClass was created on line [64] in Listing 6.21. But we need to provide a qualified name (see Figure 6.2) for the member function, which in our case is operator (). Hence, analogous to the member call scheme in Figure 3.8, a general scheme for calling members of the base class(es) is as shown in Figure 6.20.

![](bbox=[0.133, 0.508, 0.761, 0.567])

Alternatively, line [16] can be written as follows:

```
if( ( & exprParser ) ->BaseClass::operator()( good_expr ) )
```