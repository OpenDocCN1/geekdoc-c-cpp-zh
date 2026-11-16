```
ComputeWorldTransform();
}
}
```

Next, add a call to ComputeWorldTransform in Game::Update to make sure any “pending” actors (actors created while updating other actors) have their world transform calculated in the same frame where they’re created:

Click here to view code image

```
// In Game::Update (move any pending actors to mActor
for (auto pending : mPendingActors)
{
    pending ->ComputeWorldTransform();
    mActors.emplace_back(pending);
}
```

It would be nice to have a way to notify components when their owner’s world transform gets updated. This way, the component can respond as needed. To support this, first add a virtual function declaration to the base Component class: