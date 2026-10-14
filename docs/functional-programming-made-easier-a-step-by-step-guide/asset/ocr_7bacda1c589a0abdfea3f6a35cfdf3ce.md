```
import Type.Proxy (Proxy(..)) ①

type Slots = ( counter :: H.Slot Query Output Int )

_counter = Proxy :: Proxy "counter" ②
```

① Import Proxy.

② Normally, we write the Type Signature on a separate line, but this is idiomatic Halogen and terse.

We’ll use this when we add our Children to the Virtual DOM in render.

Before we embark on rendering our Children, make sure that your code is caught up.

Next, we’ll add the Children to the Virtual DOM in render: