# 8.3 Switch Statements

Rules:

+   a. The break for each case shall be indented to align with the associated case, rather than with the contents of the case code block.
b. All switch statements shall contain a default case.
c. Any case design designed to fall through to the next shall be commented to clearly explain the absence of the corresponding break.

Example:

```
switch (err)
{
    case ERR_A:
    ...
    break;
    case ERR_B:
    ...
    // Also perform the steps for ERR_C.
    case ERR_C:
    ...
    break;
    default:
    ...
    break;
}
```

Reasoning: C's switch statements are powerful constructs, but prone to errors such as omitted break statements and unhandled cases. By aligning the case labels with their break statements it is easier to spot a missing break.

Enforcement: These rules shall be enforced during code reviews.