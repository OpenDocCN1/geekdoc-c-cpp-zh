```
if (mUpdatingActors)
{
    mPendingActors.emplace_back(actor);
}
else
{
    mActors.emplace_back(actor);
}
}
```

Similarly, RemoveActor removes the actor from whichever of the two vectors it is in.

You then need to change the UpdateGame function so that it updates all the actors, as shown in Listing 2.3. After computing delta time, as discussed in Chapter 1, you then loop over every actor in mActors and call Update on each. Next, you move any pending actors into the main mActors vector. Finally, you see if any actors are dead, in which case you delete them.

# Listing 2.3 Game::UpdateGame Updating Actors

Click here to view code image

```
void Game::UpdateGame()
```