```
// pay interest according to current balance
printfn "account state = %A, interest = %A" account.State (account.PayInterest())
```

Execution result from the state pattern obtained by invoking the state function
account state = Gold, interest = 200.0
account state = Silver, interest = 80.0

In F#, one to implement a state machine with a MailboxProcessor. The F# MailboxProcessor can be viewed as a message queue. It has an asynchronous workflow as the processing logic. The asynchronous workflow will be introduced in the next chapter, and it can be thought of as a simple function executing on a background thread. The Post method is used to insert a message into the queue, and the Receive method is used to get the message out of the queue. In Listing 3-20, the variable inbox represents the message queue. When the state machine starts, it goes to state0, which is represented by the state() function, and waits for user input. The state machine will transition to another state according to the user's input.

# LISTING 3-20 State pattern with F# MailboxProcessor

```
open Microsoft.Fsharp.Control

type States =
  | State1
  | State2
  | State3

let stateMachine = new MailboxProcessor<States>(fun inbox ->
  let state() = async =
    printfn "current state is State1"
    //your operations

  //get another message and perform state transition
  let! msg = inbox.Receive()
  match msg with
    | State1 -> return!(state1())
    | State2 -> return!(state2())
    | State3 -> return!(state3())
  and state2() = async =
    printfn "current state is state2"
    //your operations

  //get another message and perform state transition
  let! msg = inbox.Receive()
  match msg with
    | State1 -> return!(state1())
    | State2 -> return!(state2())
    | State3 -> return!(state3())"
```