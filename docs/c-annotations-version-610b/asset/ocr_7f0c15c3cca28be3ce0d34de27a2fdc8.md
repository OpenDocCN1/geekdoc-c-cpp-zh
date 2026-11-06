Marshall Cline's advice can be improved, though. Here's a recipe that will effortlessly dissect even the most complex declaration:

+   1. start reading at the variable's name
+   2. read as far as possible until you reach the end of the declaration or an (as yet unmatched) closing parenthesis.
+   3. return to the point where you started reading, and read backwards until you reach the beginning of the declaration or a matching opening parenthesis.
+   4. If you reached an opening parenthesis, continue at step 2 beyond the parenthesis where you previously stopped.

Let's apply this recipe to the following (by itself irrelevant) complex declaration. Little arrows indicate how far we should read at each step and the direction of the arrow indicates the reading direction:

```
    char const *(* const *(*ip)()[])[]

                        ip          Start at the variable's name:
                                    'ip' is

                        ip)         Hitting a closing paren: revert
                        -->

                        (*ip)       Find the matching open paren:
                        <--         'a pointer to'

                        (*ip)()     The next unmatched closing par:
                            -->     'a function (not expecting
                                    arguments)'

                        (*ip)()     Find the matching open paren:
                        <--         'returning a pointer to'

                        (*ip)()[]   The next closing par:
                            -->     'an array of'

                        (* const *(*ip)()[])  Find the matching open paren:
                        <--------   'const pointers to'

                        (* const *(*ip)()[])[] Read until the end:
                            -->     'an array of'

    char const *(* const *(*ip)()[])[] Read backwards what's left:
    <----------                             'pointers to const chars'
```

Collecting all the parts, we get for `char const *(* const *(*ip)()[])[]`: *ip* is a pointer to a function (not expecting arguments), returning a pointer to an array of const pointers to an array of pointers to const chars. This is what `ip` represents; the recipe can be used to parse any declaration you ever encounter.

# ### 3.1.4 'cout', 'cin', and 'cerr'

Analogous to C, C++ defines standard input- and output streams which are available when a program is executed. The streams are:

+   - cout, analogous to stdout,