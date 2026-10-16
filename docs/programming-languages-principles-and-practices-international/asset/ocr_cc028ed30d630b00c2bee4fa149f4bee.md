into a scope and deletions on exit—is appropriate only for the simplest languages, such as C and Pascal, with a strict declaration before use requirement, and where scopes cannot be reaccessed once they have been exited during processing by a translator.

Actually, even this description does not fully cover all situations in C and Pascal. Consider, for example, struct declarations in C (or record declarations in Pascal) as given in Figure 7.17. Clearly, each of the two struct declarations in this code (lines 1–5 and 7–11 of Figure 7.17) must contain the further declarations of the data fields within each struct, and these declarations must be accessible (using the “dot” notation of member selection) whenever the struct variables themselves (x and y) are in scope. This means two things: (1) A struct declaration actually contains a local symbol table itself as an attribute (which contains the member declarations), and (2) this local symbol table cannot be deleted until the struct variable itself is deleted from the “global” symbol table of the program.

```
(1)  struct{
(2)      int a;
(3)      char b;
(4)      double c;
(5)  } x = {1, 'a',2.5};

(6)  void p(){
(7)      struct{
(8)          double a;
(9)          int b;
(10)         char c;
(11)    } y = {1.2,2, 'b'};
(12)    printf("%d, %c, %g\n",x.a,x.b,x.c);
(13)    printf("%f, %d, %c\n",y.a,y.b,y.c);
(14) }

(15) main(){
(16)    p();
(17)    return 0;
(18) }
```

Figure 7.17 Code example illustrating scope of local declarations in a C struct

Thus, inside p (line 12 of Figure 7.17), the symbol table for the preceding code might look as shown in Figure 7.18, with the symbol table attribute labeled as “symtab”).