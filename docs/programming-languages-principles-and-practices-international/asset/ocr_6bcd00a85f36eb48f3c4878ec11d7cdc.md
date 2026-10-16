```
/*
factor = primary [ "**" primary ] | "not" primary
*/
private TypeDescriptor factor(){
    TypeDescriptor t1;
    if (token.code == Token.NOT){
        token = scanner.nextToken();
        t1 = primary();
        matchTypes(t1, BOOL_TYPE, "Boolean expression expected");
    }
    else{
        t1 = primary();
        if (token.code == Token.EXPO){
            matchTypes(t1, INT_TYPE, "integer expression expected");
            token = scanner.nextToken();
            TypeDescriptor t2 = primary();
            matchTypes(t2, INT_TYPE, "integer expression expected");
        }
    }
    return t1;
}
```

This method has the following three options for returning a type descriptor:

+   1. There is no operator in the factor, so the type descriptor t1 obtained from the first call of primary is returned directly to the caller.
+   2. The operator is a leading not. Then the type descriptor t1 is returned, after matching it to BOOL_TYPE.
+   3. The operator is a binary **. Then the type descriptor t1 is returned, after matching it and the type descriptor t2, obtained from the second call to primary, to INT_TYPE.

As you can see, the type of every operand must be checked, and great care must be taken to ensure that the right type descriptor is returned. The modification of the remaining methods for parsing expressions is left as an exercise for the reader.

# 8.10.5 Processing Names: Indexed Component References and Procedure Calls

The syntax of TinyAda indexed component references and procedure calls is the same if the procedure expects at least one parameter. As shown in the previous code segment, the method name now must distinguish these two types of phrases, based on the role of the leading identifier. The code for processing the trailing phrase, which consists of a parenthesized list of expressions, can now be split into two distinct parsing methods, actualParameterPart and indexedComponent.