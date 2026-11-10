# ### 7.3.1 Program Constructor Events

The `LOAD-OF-PROGRAM` event block serves as a *program constructor*. A program constructor serves the same purpose for ABAP programs as a *constructor* serves for a class (i.e., to initialize program variables).

This type of event block is called by the ABAP runtime environment when an executable program, module pool program, function group, or subroutine pool is loaded into memory (internal session). This event is triggered only once per program execution. If the program call opens a new internal session for each call (such as when using the `SUBMIT` or `CALL TRANSACTION` statements to call another program), then the `LOAD-OF-PROGRAM` event is triggered once per every program call.

To make the program react to this event, we use the `LOAD-OF-PROGRAM` event keyword, which is the first event to be called before any other ABAP code is processed. The statements in this block allow you to initialize the data of the program.

The `LOAD-OF-PROGRAM` event is mainly used when calling external procedures to initialize the global data of the called procedure. For example, in Listing 7.10 the data object `DATE` is initialized with the current date via the `LOAD-OF-PROGRAM` event.

By maintaining the statement `DATE = SY-DATUM` under the `LOAD-OF-PROGRAM` event, we ensure that the data object `DATE` is always initialized with the current date when the program is executed.

```
~~~abap
REPORT ZCB_EXAMPLE.
DATA date TYPE d.
LOAD-OF-PROGRAM.
date = sy-datum.
~~~
```

**Listing 7.10** Using `LOAD-OF-PROGRAM` to Initialize Data

# ### 7.3.2 Reporting Events

*Reporting events* can be used in executable programs (report programs). Executable programs are event-driven. When you run an executable program, a series of events are triggered, one after the other, by the ABAP runtime environment. You can define event blocks to react to these events. Reporting events that can be used in an executable type of program include the following: