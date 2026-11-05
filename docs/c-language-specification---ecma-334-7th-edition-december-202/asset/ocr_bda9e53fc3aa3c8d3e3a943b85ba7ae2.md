Namespaces are open-ended, and two namespace declarations with the same fully qualified name (§7.8.2) contribute to the same declaration space (§7.3).

*Example:* In the following code

```
    namespace N1.N2
    {
        class A {}
    }

    namespace N1.N2
    {
        class B {}
    }
```

the two namespace declarations above contribute to the same declaration space, in this case declaring two classes with the fully qualified names N1.N2.A and N1.N2.B. Because the two declarations contribute to the same declaration space, it would have been an error if each contained a declaration of a member with the same name.

*end example*

# ## 14.4 Extern alias directives

An extern_alias_directive introduces an identifier that serves as an alias for a namespace. The specification of the aliased namespace is external to the source code of the program and applies also to nested namespaces of the aliased namespace.

```
    extern_alias_directive
        : 'extern' 'alias' identifier ';'
        ;
```

The scope of an extern_alias_directive extends over the using_directives, global_attributes and namespace_member_declarations of its immediately containing compilation_unit or namespace_body.

Within a compilation unit or namespace body that contains an extern_alias_directive, the identifier introduced by the extern_alias_directive can be used to reference the aliased namespace. It is a compile-time error for the identifier to be the word global.

The alias introduced by an extern_alias_directive is very similar to the alias introduced by a using_alias_directive. See §14.5.2 for more detailed discussion of extern_alias_directives and using_alias_directives.

alias is a contextual keyword (§6.4.4) and only has special meaning when it immediately follows the extern keyword in an extern_alias_directive.

An error occurs if a program declares an extern alias for which no external definition is provided.

*Example:* The following program declares and uses two extern aliases, X and Y, each of which represent the root of a distinct namespace hierarchy:

```
    extern alias X;
    extern alias Y;

    class Test
    {
        X::N.A a;
        X::N.B b1;
    }
```