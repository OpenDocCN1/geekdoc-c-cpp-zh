```
mBanks.emplace(name, bank);
// Load all non-streaming sample data
bank->loadSampleData();

// Get the number of events in this bank
int numEvents = 0;
bank->getEventCount(&numEvents);
if (numEvents > 0)
{
    // Get list of event descriptions in this bank
    std::vector<FMOD::Studio::EventDescription*> events(numEvents);
    bank->getEventList(events.data(), numEvents, &numEvents);
    Char eventName[maxPathLength];
    for (int i = 0; i < numEvents; i++)
    {
        FMOD::Studio::EventDescription *e = events[i];
        // Get the path of this event (like event:/Explosion2D)
        e->getPath(eventName, maxPathLength, nullptr);
        // Add to event map
        mEvents.emplace(eventName, e);
    }
}
}
```