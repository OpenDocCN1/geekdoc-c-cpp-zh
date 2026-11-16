```
const int maxPathLength = 512;

if (result == FMOD_OK)
{
    // Add bank to map
    mBanks.emplace(name, bank);

    // Load all non-streaming sample data
    bank ->loadSampleData();

    // Get the number of events in this bank
    int numEvents = 0;
    bank ->getEventCount(&numEvents);

    if (numEvents > 0)
    {
        // Get list of event descriptions in this ba
        std::vector<FMOD::Studio::EventDescription*>
        bank ->getEventList(events.data(), numEvents
        char eventName[maxPathLength];
        for (int i = 0; i < numEvents; i++)
        {
            FMOD::Studio::EventDescription* e = event
            // Get the path of this event (like event
        }
    }
}
```