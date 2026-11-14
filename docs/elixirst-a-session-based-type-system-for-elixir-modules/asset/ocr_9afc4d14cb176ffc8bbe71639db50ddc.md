![](bbox=[0.31, 0.06, 0.69, 0.25])

```
defmodule Counter do
  use ElixirST

  @session "counter" = ?{:incr(number).counter,
                    ?stop())).{value|number.end}

  @spec server(pid, number) :: atom
  def server(client, number) do
    receive do
      {:incr, value} -> server(client, total + value)
      {:stop} -> terminate(client, total)
    end
  end

  @spec terminate(pid, number) :: atom
  def terminate(client, total) do
    send(client, {:value, total})
    :ok
  end

  @dual "counter"
  @spec client(pid) :: number
  def client(server) do
    ...
  end
end
```

Listing 2: Counter annotated with session types.

Concretely, it can repeatedly make a _choice_ (_i.e._, \(\oplus\)) to send one of two labels, either `increment` or `stop`. The former ensures that it receives back to the beginning, while the latter results in the client receiving a value of type `number`.

This paper proposes an approach whereby module definitions are augmented with a `@session` annotation for functions, as shown in Listing 2. Whereas line 4 requires the `public` function `server` to adhere to the session type `counter`, no session annotation is required for the `private` function `terminate` on line 15. Lines 22-24 present a case in which the client code is defined as a public function within the same module; in such a case, we can annotate it with the `@dual` information on line 20.

Our proposed session type annotations serve two important purposes. On the one hand, they provide a high-level (yet formal) specification as to how a public function is to be interacted with, without the need to look inside its implementation, as in the case of line 4. For instance, by inspecting the `counter` session type on line 4 of Listing 2, one can immediately tell that a process running function `server` accepts two types of messages with labels `incr` or `stop`. On the other hand, they allow function implementations to be typechecked against such specifications. _E.g._, we are able to statically check that the function `server` (and its ancillary function `terminate`) adheres to the protocol dictated by session type `counter` on line 4. We can also reject the problematic `client` implementation given in Listing 3 at compile-time, on the grounds that it violates the dual session type of `counter`. Concretely, the client selects an illegal choice `decr` on line 23, since the server cannot handle an incoming message labelled `decr`. The client also expects to receive a value with a `number` (line 26) after "forgetting" to send a termination request (_i.e._, a message with a `stop` label). Both cases breach the `counter` protocol.

# 3. A formal analysis

We introduce a core Elixir subset and define the typing rules for the ElixirST type system.