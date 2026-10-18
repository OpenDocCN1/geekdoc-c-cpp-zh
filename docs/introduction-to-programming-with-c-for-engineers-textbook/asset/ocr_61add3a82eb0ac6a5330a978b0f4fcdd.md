The SyntaxTree_Test function in Listing 6.28, line [1], operates with the ExpressionTreeBuilderInterpreter class from Listing 6.21. The exprParser object of this class is created on line [4]. The expression to be processed is defined on line [6].

Line [8] invokes operator () with good_expr as its argument. This does the parsing, as described in Section 6.6.5. If false is returned, then a syntax error was encountered. In this case, on lines [10, 11], the correct message is output, indicating a possible place where the interpreter got stuck, and the procedure ends.

On the other hand, if the expression is parsed with success, then on line [18], theRoot pointer is attached to the root of the syntax tree. We do not know what the type of this node is, but this does not stop us from calling the Accept virtual function on line [23] with the PrintVisitor object as its parameter. This is polymorphism again. As a result, the structure of the syntax tree is printed in the terminal window, as we will show.

```
```cpp
void SyntaxTree_Test( void )
{
    ExpressionTreeBuilderInterpreter exprParser;

    string good_expr( "((1+2)*((3-(4+5))/(6-7)))" );

    if( exprParser( good_expr ) == false )
    {
        cout << "Syntax error!\\n" << good_expr << "\\n";
        cout << std::string( exprParser.GetCurPos(), ' ' ) << '^' << "\\nExiting\\n";
        return;
    }

    // Here we can do something with the tree e.g. launch a visitor

    // Take a pointer to the root of the tree
    NodePtr     theRoot { exprParser.GetRoot() };
    assert( theRoot );

    // Print structure of the parsing tree
    theRoot->Accept( PrintVisitor() ); // Pass a temporary object as an argument

    // Let’s make a clone of the tree - e.g. to use it in a separate thread
    Node_UP    theSecondTree { theRoot->Clone() };

    // Evaluate the expression
    EvalVisitor evalVisitor;
    try
    {
        theSecondTree->Accept( evalVisitor );    // Can throw on zero division
        std::cout << "Val = " << evalVisitor.GetValue() << endl;
    }
    catch( std::exception & e )
    {
        std::cerr << e.what() << endl;
    }
}
```
```