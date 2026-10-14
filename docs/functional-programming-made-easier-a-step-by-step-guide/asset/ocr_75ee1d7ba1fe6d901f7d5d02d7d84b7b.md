|  |  |
|---|---|
| ExceptT | runExceptT |
| WriterT | runWriterT |
| StateT | runStateT |
| Identity | unwrap |

We'll use the REPL to help us determine the final result based on how we'd run this Stack:

```
$ npx spago repl
PSCi, version 0.14.1
Type :? for help

> import Prelude
> import Control.Monad.State.Trans
> import Control.Monad.Writer.Trans
> import Control.Monad.Except.Trans
> :t flip runStateT unit <<< runWriterT <<< runExceptT ①
forall t17 t18 t20 t9. ExceptT t20 (WriterT t17 (StateT Unit t9)) t18 -> t9 (Tuple (Tuple (Either t20 t18) t17) Unit)
```

① We're using unit as the Initial State.

Let's clean up that Type Signature a bit:

```
-- original
flip runStateT unit <<< runWriterT <<< runExceptT ①
:: forall t17 t18 t20 t9
  . ExceptT t20 (WriterT t17 (StateT Unit t9)) t18 ②
-> t9 (Tuple (Tuple (Either t20 t18) t17) Unit)
-- cleaned up
flip runStateT s <<< runWriterT <<< runExceptT ③
:: ∀ e w s m a
  . ExceptT e (WriterT w (StateT s m)) a ④
-> m (Tuple (Tuple (Either e a) w) s) ④
-- return Value
m (Tuple (Tuple (Either e a) w) s) ⑤
```