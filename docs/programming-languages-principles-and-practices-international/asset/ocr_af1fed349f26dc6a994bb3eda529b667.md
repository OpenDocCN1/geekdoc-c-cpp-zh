10.18 Draw the stack of activation records for the following Ada program (a) after the first call to procedure b; (b) after the second call to procedure b. Show the control links and the access links for each activation record. (c) Indicate how b is found in procedure c.

```
procedure env is

    procedure a is

        procedure b is

            procedure c is
            begin
                b;
            end c;

            begin
                c;
            end b;

        begin
            b;
        end a;

    begin
        a;
    end env;
```

10.19 The following Ada program contains a function parameter.
(a) Draw the stack of activation records after the call to g in p. (b) What does the program print and why?

```
with Text_IO; use Text_IO;
with Ada.Integer_Text_IO;
use Ada.Integer_Text_IO;

procedure params is
    procedure q is
    type IntFunc is access function (n:integer) return integer;
    m: integer := 0;

    function f (n: integer) return integer is
    begin
        return m + n;
    end f;
    procedure p (g: IntFunc) is
```

(continues)