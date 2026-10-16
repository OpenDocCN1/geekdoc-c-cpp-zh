
By making the string NUMBER uppercase in the new grammar, we are saying that it is not a token to be recognized literally, but one whose structure is determined by the scanner. The structure of such tokens must then be specified as part of the lexical conventions of the language. As noted in Section 6.1, the structure of such tokens can be specified using regular expressions. However, many language designers choose to include the structure of such tokens as part of the grammar, with the understanding that an implementor may include these in the scanner instead of the parser. Thus, a description of a language using BNF, EBNF, or syntax diagrams may include not only the syntax but most of the lexical structure (or **lexics**) of a programming language as well. The boundary, therefore, between syntactic and lexical structure is not always clearly drawn, but depends on the point of view of the designer and implementor.

The same is true for syntax and semantics. We have been taking the approach that syntax is anything that can be defined with a context-free grammar and semantics is anything that cannot. However, authors include properties that we would call semantic as syntactic properties of a language. Examples include such rules as declaration before use for variables and no redeclaration of identifiers within a procedure. These are rules that are context sensitive and cannot be written as context-free rules. Hence we prefer to think of them as semantic rather than syntactic rules.

Another conflict between syntax and semantics arises when languages require certain strings to be **predefined identifiers** rather than **reserved words**. Recall from Section 6.1 that reserved words are fixed strings of characters that are tokens themselves and that cannot be used as identifiers. By contrast, a predefined identifier is a fixed string that is given a predefined meaning in a language, but this meaning can be changed by redefining it within a program. As we have noted, the strings *if*, *while*, and *do* are reserved words in C, Java, and Ada. However, in Ada, all of the basic data type names, such as *integer* and *boolean*, are predefined identifiers that can be redefined. For example, the following declaration in Ada is perfectly legal:

```text
integer: boolean;
```

After this declaration, the name *integer* has become a variable of type *boolean*. (You’re not alone if you find this confusing.)

C, C++, and Java, on the other hand, make the basic types such as *int*, *double*, and *bool* (in C++) or *boolean* (in Java) reserved words that cannot be redefined. This is probably a better approach, since these names have a fixed semantics in every program that we would hardly want to change even if we could.

Finally, syntax and semantics can become interdependent in languages when semantic information must be used to distinguish ambiguous parsing situations. A simple situation where this occurs is in C, where type names and variable names must be distinguishable during parsing. Consider, for example, the C expression:

```text
(x)-y
```

If x is a type name, this is a cast of the value −y to type x. However, if x is a variable name, then this is subtraction of y from x. Thus, a parser must have context information on identifiers available to disambiguate such situations. One might view this as a design flaw in the grammar of C. (Java has the same problem, but not Ada.) However, it is a relatively easy problem to overcome in practice, as you will see in later chapters.

## 6.8 Case Study: Building a Syntax Analyzer for TinyAda

We conclude this chapter by developing a parser for a small language that is similar in some ways to the Ada programming language. This little language, called TinyAda, is large enough to illustrate the syntactic features of many high-level languages, yet small enough to require a medium-sized programming project. In this section, we inaugurate the project by discussing a simple syntax analyzer. The next few chapters revisit the project to add code to analyze some semantics as well.

An EBNF grammar for TinyAda is shown in Figure 6.27. Note the semantic qualifiers, such as <type>, enclosed in angle brackets. You can ignore these for now, but we will return to them in the next few chapters.

```text
In the following grammar

=     means "is defined as"
" "   enclose literal items
[ ]   enclose items which may be omitted
{ }   enclose items which may appear zero or more times
|     indicates a choice
( )   are used for grouping required choices
< >   enclose semantic qualifications

subprogramBody =
        subprogramSpecification "is"
        declarativePart
        "begin" sequenceOfStatements
        "end" [ <procedure>identifier ] ";"

declarativePart = { basicDeclaration }

basicDeclaration = objectDeclaration | numberDeclaration
                  | typeDeclaration | subprogramBody

objectDeclaration =
        identifierList ":" typeDefinition ";"

numberDeclaration =
        identifierList ":" "constant" ":=" <static>expression ";"

identifierList = identifier { "," identifier }

typeDeclaration = "type" identifier "is" typeDefinition ";"

typeDefinition = enumerationTypeDefinition | arrayTypeDefinition
                | range | <type>name

range = "range" simpleExpression ".." simpleExpression

index = range | <type>name

enumerationTypeDefinition = "(" identifierList ")"

arrayTypeDefinition = "array" "(" index { "," index } ")" "of" <type>name

subprogramSpecification = "procedure" identifier [ formalPart ]

formalPart = "(" parameterSpecification { "," parameterSpecification } ")"

parameterSpecification = identifierList ":" mode <type>name

mode = [ "in" ] | "in" "out" | "out"

sequenceOfStatements = statement { statement }

statement = simpleStatement | compoundStatement

simpleStatement = nullStatement | assignmentStatement
                 | procedureCallStatement | exitStatement

compoundStatement = ifStatement | loopStatement

nullStatement = "null" ";"

assignmentStatement = <variable>name ":=" expression ";"

ifStatement =
        "if" condition "then" sequenceOfStatements
        { "elsif" condition "then" sequenceOfStatements }
        [ "else" sequenceOfStatements ]
        "end" "if" ";"

loopStatement =
        [ iterationScheme ] "loop" sequenceOfStatements "end" "loop" ";"

iterationScheme = "while" condition

exitStatement = "exit" [ "when" condition ] ";"

procedureCallStatement = <procedure>name [ actualParameterPart ] ";"

actualParameterPart = "(" expression { "," expression } ")"

condition = <boolean>expression

expression = relation { "and" relation } | relation { "or" relation }

relation = simpleExpression [ relationalOperator simpleExpression ]

simpleExpression =
    [ unaryAddingOperator ] term { binaryAddingOperator term }

term = factor { multiplyingOperator factor }

factor = primary [ "**" primary ] | "not" primary

primary = numericLiteral | stringLiteral | name | "(" expression ")"

name = identifier [ indexedComponent ]

indexedComponent = "(" expression { "," expression } ")"

relationalOperator = "=" | "/=" | "<" | "<=" | ">" | ">="

binaryAddingOperator = "+" | "-"

unaryAddingOperator = "+" | "-"

multiplyingOperator = "*" | "/" | "mod"
```

**Figure 6.27** An EBNF grammar for TinyAda

As you can see from the grammar, TinyAda includes several kinds of declarations (constant, variable, type, and procedure), statements (assignment, selection, loop, and procedure call), and expressions. The top-level phrase in this little language, called subprogramBody, is a procedure declaration, which might serve the same role for a TinyAda program as the main function of the C language does in the execution of a program. Note also that the rules for declarations, statements, and expressions are indirectly recursive, allowing for nested declarations, statements, and expressions.

Figure 6.28 shows a short TinyAda program, which includes two procedure declarations and several constant declarations, type declarations, variable declarations, statements, and expressions.

```text
procedure TEST is

    COLUMN_MAX : constant := 10;
    ROW_MAX : constant := COLUMN_MAX;
    type COLUMN_INDEX is range 1..COLUMN_MAX;
    type ROW_INDEX is range 1..ROW_MAX;
    type MATRIX is array(COLUMN_INDEX, ROW_INDEX) of INTEGER;
```

**Figure 6.28** A TinyAda program (continues)
