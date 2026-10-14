done some of that already, even though I’m pretty sure there will be more.

So, throw away the placeholder test and replace with the main functionality of this program in a new Function called test. When it comes to forking Fibers, call your Publisher randomGenerator and your Subscriber logger.

To get your code to compile, write those functions but just stub them out, i.e. make a do-nothing version of them. In this case, you can just return pure unit for now.

Give it a try and read on once you’ve finished or need a little help.

First, we always start with the Type Signature:

```
test :: Effect Unit
```

Next, the implementation as a do block:

```
test :: Effect Unit
test = do
  ???
```

Now, we should first create our Bus, which we know we can do in Effect:

```
import Effect.Aff.Bus as Bus ①

test :: Effect Unit
test = do
  bus <- Bus.make
  ???
```

① Import qualified so we don’t have name collision on simple names like make, read and write.

Next, we’re going to fork our Publishers and Subscribers. We could do this with runAff, but we don’t need their return Values since there will be none.

So, we’re going to use forkAff instead which means we’ll need to be in Aff to do that. So, we’ll need to add launchAff_: