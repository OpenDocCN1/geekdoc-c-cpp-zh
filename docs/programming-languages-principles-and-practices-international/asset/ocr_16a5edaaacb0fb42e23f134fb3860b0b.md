Note that the **area** function consists of two clauses, one for rectangles and the other for circles. When the programmer applies the **area** function to a value, the interpreter matches this value to the header of the appropriate clause of the **area** function as defined in the **geometry** module. Note that the form of the argument to the function must match the header of one of the two clauses specified in the module, or an error is raised. When an argument matches a function clause, the variables in the header of this clause are bound to the corresponding values contained in the argument. The clause’s code following the → symbol is then executed in the context of these bindings. Here is an example session that compiles and tests the **geometry** module:

```
1> c(geometry).
{ok, geometry}
2> geometry:area({rectangle, 8, 4}).
32
3> geometry:area({circle, 3.5}).
38.4844775
```

Before we examine how Erlang can execute this code in parallel with other code, we need to see how functions can be passed as arguments to other functions. Mapping, which we have seen before in other functional languages, illustrates the use of function arguments. Erlang’s standard **lists** module includes a map function for mapping other functions onto lists of arguments. A function argument to **lists:map** (or to any other function) must be a special type of Erlang function called a fun. The following session shows the use of fun in three applications of **lists:map**:

```
1> lists:map(fun(N) -> 2 * N end, [2, 4, 6]).
[4, 8, 12]
2> Double = fun(N) -> 2 * N end.
#Fun<erl_eval.6.57006448>
3> lists:map(Double, [2, 4, 6]).
[4, 8, 12]
4> lists:map(fun math:sqrt/0, [4, 9, 16]).
[2, 3, 4]
```

At prompt 1, fun is used, like lambda in Lisp, to build an anonymous function to pass as an argument to **lists:map**. At prompt 2, the variable Double is bound to a fun. This variable is then passed as an argument to **lists:map** at prompt 3. At prompt 4, the standard math function sqrt is wrapped in a fun before it is passed as an argument to **lists:map** at prompt 4.

Armed with these basic ideas, we are ready to see how Erlang supports parallel programming. An Erlang process is a very lightweight software object that runs independently of any other process and communicates with other processes by sending and receiving messages. The essential operations on processes are **spawn**, which creates a new process; **send**, for sending messages to other processes; and **receive**, for receiving messages. Table 13.1 describes the syntax and semantics of these operations in Erlang.