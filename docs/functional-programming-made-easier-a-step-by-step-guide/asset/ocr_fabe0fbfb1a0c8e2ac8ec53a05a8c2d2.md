```
nested :: ReaderT { debug :: Boolean }
    (StateT { count :: Int } (WriterT String Identity)) Unit
nested = ... ①

runTopLayer :: StateT { count :: Int } (WriterT String Identity) Unit ②
runTopLayer = nested
  #  flip runReaderT { debug: false }

runTop2Layers
  :: WriterT String Identity (Tuple Unit { count :: Int } ) ③
runTop2Layers = nested
  #  flip runReaderT { debug: false }
  >>> flip runStateT { count: 0 }

runTop3Layers
  :: Identity (Tuple (Tuple Unit { count :: Int } ) String ) ④
runTop3Layers = nested
  #  flip runReaderT { debug: false }
  >>> flip runStateT { count: 0 }
  >>> runWriterT

runTop4Layers :: Tuple (Tuple Unit { count :: Int } ) String ⑤
runTop4Layers = nested
  #  flip runReaderT { debug: false }
  >>> flip runStateT { count: 0 }
  >>> runWriterT
  >>> unwrap
```

① Implementation details here don’t matter

② Runs the top Layer of the Monad Stack. Notice that ReaderT is gone from the returned Stack.

③ Runs the top 2 Layers of the Monad Stack. Notice that StateT is gone from the returned Stack.

④ Runs the top 3 Layers of the Monad Stack. Notice that WriterT is gone from the returned Stack.

⑤ Runs all 4 Layers of the Monad Stack. Notice that Identity is gone from the return Value.

# 20.1. Reducing the need for lift

The biggest problem with the following code is that there are too many calls to lift and we have to lift multiple times depending on how far down the Stack a Monad resides: