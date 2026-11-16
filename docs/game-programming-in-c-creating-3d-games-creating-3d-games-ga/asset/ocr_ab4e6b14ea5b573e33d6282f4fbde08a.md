```
e ->getPath(eventName, maxPathLength, nul
// Add to event map
mEvents.emplace(eventName, e);
}
}
}
}
```

Similarly, you create an `AudioSystem::UnloadBank` function. This function first removes all the bank's events from the `mEvents` banks, unloads the sample data, unloads the bank, and removes the bank from the `mBanks` map.

For easy cleanup, you also create an `AudioSystem::UnloadAllBanks` function. This function just unloads all banks and clears out `mEvents` and `mBanks`.

Every FMOD Studio project has two default bank files named "Master Bank.bank" and "Master Bank.strings.bank". The FMOD Studio runtime does not have access to any other banks or events unless it loads in the two master banks first. Because the master banks always exist, you load them in `AudioSystem::Initialize` with the following code: