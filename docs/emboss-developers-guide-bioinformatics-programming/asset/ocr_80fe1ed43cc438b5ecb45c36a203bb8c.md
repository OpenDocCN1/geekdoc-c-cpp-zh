```
AjBool ajStrMatchWildC (const AjPStr thys, const char* text);
AjBool ajStrMatchWildS (const AjPStr thys, const AjPStr wild);
AjBool ajStrMatchWildCaseC (const AjPStr thys, const char* text);
AjBool ajStrMatchWildCaseS (const AjPStr thys, const AjPStr wild);
AjBool ajStrMatchWildWordC (const AjPStr str, const char* text);
AjBool ajStrMatchWildWordS (const AjPStr str, const AjPStr text);
AjBool ajStrMatchWildWordCaseC (const AjPStr str, const char* text);
AjBool ajStrMatchWildWordCaseS (const AjPStr str, const AjPStr text);
AjBool ajStrMatchWordAllS(const AjPStr str, const AjPStr str2);
AjBool ajStrMatchWordOneS(const AjPStr str, const AjPStr str2);
AjBool ajStrPrefixC(const AjPStr str, const char* txt2);
AjBool ajStrPrefixS(const AjPStr str, const AjPStr str2);
AjBool ajStrPrefixCaseC (const AjPStr str, const char* pref);
AjBool ajStrPrefixCaseS (const AjPStr str, const AjPStr pref);
AjBool ajStrSuffixC (const AjPStr thys, const char* suff);
AjBool ajStrSuffixS (const AjPStr thys, const AjPStr suff);
AjBool ajStrSuffixCaseC (const AjPStr str, const char* pref);
AjBool ajStrSuffixCaseS (const AjPStr str, const AjPStr pref);
```

Let us examine how the name rules work for the function ajStrMatchWildWordCaseS. This is the most difficult example you are likely to find:

+   1. @nam1rule aj Function belongs to the AJAX library.
+   
+   This rule in the file section defines the first function name component to be aj. All functions in the AJAX library have this prefix.

+   2. @nam2rule Str Function is for manipulating strings.
+   
+   This rule in the data section for AJAX (AjPStr) strings defines the second function name component to be Str. All functions in the AJAX string library (ajstr.h/c) that operate on AJAX (AjPStr) strings have the prefix ajStr.

+   3. @nam3rule Match Compare two complete strings.
+   
+   This rule in the standard section for ‘comparison’ functions defines the third function name component to be Match. The free text indicates that all functions with the prefix ajStrMatch* are for comparing two complete strings.

+   4. @nam4rule MatchWild Comparison using wildcard characters.
+   
+   This rule defines the fourth function name component to be Wild and indicates that functions with the prefix ajStrMatchWild* compare two (complete) strings using wildcard characters.

+   5. @nam5rule MatchWildWord Case-sensitive wildcard comparison of first words within two strings.
+   
+   This rule defines the fifth function name component to be Word and indicates that functions with the prefix ajStrMatchWildWord compare two complete strings using wildcard characters, using only the first words within the two strings.

+   6. @nam6rule MatchWildWordCase Case - insensitive wildcard comparison of first words within two strings.
+   
+   This rule defines the sixth function name component to be Case and indicates that functions with the prefix ajStrMatchWildWordCase compare two complete strings using wildcard characters, using only the first words within the two strings, with case-insensitivity.