# ## C.9.2 Implicit declarations

Examples of these would be:

```
extern fubar(int x);
main(int argc, char **argv)
```

Do not use them. Always specify what a function should return. This is better:

```
extern int fubar(int x);
int main(int argc, char **argv)
```

# ## C.9.3 Function and parameter names

Application function names should be:

+   - Prepended with the application name (lower-case) followed by an underscore: applicationname_FunctionName
+   - Meaningful
+   - As short as possible
+   - Given in ‘Sentence case’ where the name has more than one word
+   - Use alphabetic characters only (other than the single underscore).

for example:

```
static void abiview_TextDisplay(AjPGraph graphs, ajint nstart, ajint nstop,
                                const AjPStr nseq, float tmax, float scale);
static ajint abiview_getResColour(char B);
```

Library function and function parameter names follow all but the first of the above conventions, additionally:

+   - All AJAX public (external) functions should begin with aj
+   - All NUCLEUS public (external) functions should begin with emb.

for example:

```
AjBool ajStrAssignSubs(AjPStr* Pstr, const AjPStr str,
                         ajint pos1, ajint pos2);
double embIepPhFromHconc (double H);
```