# Table 6.1. Ada/SPARK assertions

| Aspect/Pragma | Supported in SPARK | SPARK only | Cross reference |
|---|---|---|---|
| Assert | Yes | No | Section 6.3.1 |
| Assert_And_Cut | Yes | Yes | Section 6.3.2 |
| Assume | Yes | Yes | Section 6.3.3 |
| Contract_Cases | Yes | Yes | Section 6.2.6 |
| Dynamic_Predicate | No | No | Section 6.2.5 |
| Initial_Condition | Yes | Yes | Section 6.2.2 |
| Loop_Invariant | Yes | Yes | Section 6.4 |
| Loop_Variant | Yes | Yes | Section 6.5 |
| Post | Yes | No | Section 6.2.2 |
| Pre | Yes | No | Section 6.2.1 |
| Refined_Post | Yes | Yes | Section 6.2.3 |
| Static_Predicate | Yes | No | Section 6.2.5 |
| Type_Invariant | No | No | Section 6.2.4 |

properties of types are formally specified in the program itself by way of assertions written by the software designer. We use the term *assertion* to refer to a specific condition encoded into the program and reserve the term *contracts* to refer to the abstract concept of using assertions to formalize a program’s behavior.

In Ada, assertions created during program design are executable. During runtime they can be checked to ensure that the behaviors specified by the designers are being realized. The SPARK tool goes beyond this dynamic checking and endeavor to statically prove that none of the assertions will ever fail.

Table 6.1 shows all the assertion forms available to an Ada/SPARK programmer with references to where we discuss each form in more detail. At the time of this writing not all assertion forms that exist in Ada are yet supported by SPARK. Unsupported assertions are indicated as such in the table. Furthermore, SPARK adds some assertion forms that are not part of standard Ada. Those that are SPARK specific are also indicated in the table.

Whenever a program unit is compiled, some *assertion policy* is in effect. The Ada standard defines only two such policies, Check and Ignore, although compilers are allowed to provide additional policies.

If the assertion policy is Check, then any assertion that fails (evaluates to false) causes an Assertion_Error exception from the Ada.Assertions package to be raised. It is important to understand that this check occurs at runtime and recovery must be done at runtime, for example, by way of a suitable exception handler. In this respect, assertions are similar to the runtime errors described