Before we implement this, we should install purescript-halogen and purescript-halogen-css:

```
npx spago install halogen ① ②
npx spago build ③
```

① Install both packages.

② Once halogen-css gets updated for version 14 of the compiler, we could install it here as well using: npx spago install halogen halogen-css instead.

③ Build project so we won’t get errors in the editor when we import Halogen modules.

Ignore the warnings for now.

Next, make sure you’re working in Capability.Navigate and then write the code for the Navigate Instance for HalogenM.

Remember that HalogenM state action slots output m is the Monad, which Navigate calls m.

Once your done, continue reading.

First, we’ll start coding the instance defintion:

```
import Halogen (HalogenM) ①

instance navigateHalogenM
  :: Navigate m route ②
  => Navigate (HalogenM state action slots output m) route where ③
```

① Added this import.

② HalogenM’s underlying Monad must support Navigate, hence, the Constraint. In our case, this will be AppM.

③ Notice that we’re not using a, i.e. the final Type Parameter to HalogenM. That’s because everything that preceeds it is a Monad.

The Type Signature says that as long as the underlying Monad, in our case AppM, has a Navigate Instance, then HalogenM will.

Next, we’ll add the navigate implementation by simply lifting the underlying Monad’s navigate: