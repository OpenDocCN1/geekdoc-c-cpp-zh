```
```
switch (i) {
    case 0:
        CaseZero();
    case 1:
        CaseZeroOrOne();
    default:
        CaseAny();
}
```
```

results in a compile-time error. When execution of a switch section is to be followed by execution of another switch section, an explicit goto case or goto default statement shall be used:

```
```
switch (i) {
    case 0:
        CaseZero();
        goto case 1;
    case 1:
        CaseZeroOrOne();
        goto default;
    default:
        CaseAny();
        break;
}
```
```

end example]

Multiple labels are permitted in a switch-section. [Example: The example

```
```
switch (i) {
    case 0:
        CaseZero();
        break;
    case 1:
        CaseOne();
        break;
    case 2:
    default:
        CaseTwo();
        break;
}
```
```

is valid. The example does not violate the “no fall through” rule because the labels case 2: and default: are part of the same switch-section. end example]

[Note: The “no fall through” rule prevents a common class of bugs that occur in C and C++ when break statements are accidentally omitted. For example, the sections of the switch statement above can be reversed without affecting the behavior of the statement:

```
```
switch (i) {
    default:
        CaseAny();
        break;
    case 1:
        CaseZeroOrOne();
        goto default;
    case 0:
        CaseZero();
        goto case 1;
}
```
```

end note]

[Note: The statement list of a switch section typically ends in a break, goto case, or goto default statement, but any construct that renders the end point of the statement list unreachable is permitted. For example, a while statement controlled by the Boolean expression true is known to never reach its end point. Likewise, a throw or return statement always transfers control elsewhere and never reaches its end point. Thus, the following example is valid: