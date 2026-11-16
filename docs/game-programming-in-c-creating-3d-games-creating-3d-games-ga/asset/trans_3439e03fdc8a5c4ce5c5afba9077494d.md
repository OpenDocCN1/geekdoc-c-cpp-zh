

```cpp
mSystem->getLowLevelSystem(&mLowLevelSystem);
```

```cpp
class AudioSystem* mAudioSystem;
```

```cpp
// Map of loaded banks
std::unordered_map<std::string, FMOD::Studio::Bank*> mBanks;
// Map of event name to EventDescription
std::unordered_map<std::string, FMOD::Studio::EventDescription*> mEvents;
```

```cpp
void AudioSystem::LoadBank(const std::string& name)
{
    // Prevent double-loading
    if (mBanks.find(name) != mBanks.end())
    {
        return;
    }

    // Try to load bank
    FMOD::Studio::Bank* bank = nullptr;
    FMOD_RESULT result = mSystem->loadBankFile(
        name.c_str(),    // File name of bank
        FMOD_STUDIO_LOAD_BANK_NORMAL,    // Normal loading
        &bank    // Save pointer to bank
    );

    const int maxPathLength = 512;
    if (result == FMOD_OK)
    {
        // Add bank to map
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
}
```

```cpp
// Load the master banks (strings first)
LoadBank("Assets/Master Bank.strings.bank");
LoadBank("Assets/Master Bank.bank");
```

```cpp
void AudioSystem::PlayEvent(const std::string& name)
{
    // Make sure event exists
    auto iter = mEvents.find(name);
    if (iter != mEvents.end())
    {
        // Create instance of event
        FMOD::Studio::EventInstance* event = nullptr;
        iter->second->createInstance(&event);
        if (event)
        {
            // Start the event instance
            event->start();
            // Release schedules destruction of the event
            // instance when it stops.
            // (Non-looping events automatically stop.)
            event->release();
        }
    }
}
```

```cpp
std::unordered_map<unsigned int,
    FMOD::Studio::EventInstance*> mEventInstances;
```

```cpp
SoundEvent AudioSystem::PlayEvent(const std::string& name)
{
    unsigned int retID = 0;
    auto iter = mEvents.find(name);
    if (iter != mEvents.end())
    {
        // Create instance of event
        FMOD::Studio::EventInstance* event = nullptr;
        iter->second->createInstance(&event);
        if (event)
        {
            // Start the event instance
            event->start();
            // Get the next id, and add to map
            sNextID++;
            retID = sNextID;
            mEventInstances.emplace(retID, event);
        }
    }
    return SoundEvent(this, retID);
}
```

```cpp
void AudioSystem::Update(float deltaTime)
{
    // Find any stopped event instances
    std::vector<unsigned int> done;
    for (auto iter : mEventInstances)
    {
        FMOD::Studio::EventInstance* e = iter.second;
        // Get the state of this event
        FMOD_STUDIO_PLAYBACK_STATE state;
        e->getPlaybackState(&state);
        if (state == FMOD_STUDIO_PLAYBACK_STOPPED)
        {
            // Release the event and add id to done
            e->release();
            done.emplace_back(iter.first);
        }
    }
    // Remove done event instances from map
    for (auto id : done)
    {
        mEventInstances.erase(id);
    }
    // Update FMOD
    mSystem->update();
}
```

```cpp
class SoundEvent
{
public:
    SoundEvent();
    // Returns true if associated FMOD event instance exists
    bool IsValid();
    // Restart event from beginning
    void Restart();
    void SetEvent();
    // Stop (this) event
    void Stop(bool allowFadeOut = true);
    // Setters
    void SetPaused(bool pause);
    void SetVolume(float value);
    void SetPitch(float value);
    void SetParameter(const std::string& name, float value);
    // Getters
    bool GetPaused() const;
    float GetVolume() const;
    float GetPitch() const;
    float GetParameter(const std::string& name);
protected:
    // Make this constructor protected and AudioSystem a friend
    // so that only AudioSystem can access this constructor.
    friend class AudioSystem;
    SoundEvent(class AudioSystem* system, unsigned int id);
private:
    class AudioSystem* mSystem;
    unsigned int mID;
};
```

```cpp
void SoundEvent::SetPaused(bool pause)
{
    auto event = mSystem ?
        mSystem->GetEventInstance(mID) : nullptr;
    if (event)
    {
        event->setPaused(pause);
    }
}
```

```cpp
mMusicEvent = mAudioSystem->PlayEvent("event:/Music");
```

```cpp
mMusicEvent.SetPaused(!mMusicEvent.GetPaused());
```

```cpp
FMOD_VECTOR VecToFMOD(const Vector3& in)
{
// Convert from our coordinates (+x forward, +y right, +z up)
// to FMOD (+z forward, +x right, +y up)
FMOD_VECTOR v;
v.x = in.y;
v.y = in.z;
v.z = in.x;
return v;
}
```

```cpp
void AudioSystem::SetListener(const Matrix4& viewMatrix)
{
    // Invert the view matrix to get the correct vectors
    Matrix4 invView = viewMatrix;
    invView.Invert();
    FMOD_3D_ATTRIBUTES listener;
    // Set position
    listener.position = VecToFMOD(invView.GetTranslation());
    // In the inverted view, third row is forward
    listener.forward = VecToFMOD(invView.GetZAxis());
    // In the inverted view, second row is up
    listener.up = VecToFMOD(invView.GetYAxis());
    // Set velocity to zero (fix if using Doppler effect)
    listener.velocity = {0.0f, 0.0f, 0.0f};
    // Send to FMOD (0 = only one listener)
    mSystem->setListenerAttributes(0, &listener);
}
```

```cpp
bool SoundEvent::is3D() const
{
    bool retVal = false;
    auto event = mSystem ? mSystem->GetEventInstance(mID) : nullptr;
    if (event)
    {
        // Get the event description
        FMOD::Studio::EventDescription* ed = nullptr;
        event->getDescription(&ed);
        if (ed)
        {
            ed->is3D(&retVal); // Is this 3D?
        }
    }
    return retVal;
}
```

```cpp
void SoundEvent::Set3DAttributes(const Matrix4x4& worldTrans)
{
    auto event = mSystem ? mSystem->GetEventInstance(mID) : nullptr;
    if (event)
    {
        FMOD_3D_ATTRIBUTES attr;
        // Set position, forward, up
        attr.position = VecToFMOD(worldTrans.GetTranslation());
        // In world transform, first row is forward
        attr.forward = VecToFMOD(worldTrans.GetXAxis());
        // Second row is up
        attr.up = VecToFMOD(worldTrans.GetYAxis());
        // Set velocity to zero (fix if using Doppler effect)
        attr.velocity = { 0.0f, 0.0f, 0.0f };
        event->set3DAttributes(&attr);
    }
}
```

```cpp
class AudioComponent : public Component
{
public:
    AudioComponent(class Actor* owner, int updateOrder = 200);
    ~AudioComponent();

    void Update(float deltaTime) override;
    void OnUpdateWorldTransform() override;

    SoundEvent PlayEvent(const std::string& name);
    void StopAllEvents();

private:
    std::vector<SoundEvent> mEvents2D;
    std::vector<SoundEvent> mEvents3D;
};
```

```cpp
SoundEvent AudioComponent::PlayEvent(const std::string& name)
{
    SoundEvent e = mOwner->GetGame()->GetAudioSystem()->PlayEvent(name);
    // Is this 2D or 3D
    if (e.Is3D())
    {
        mEvents3D.emplace_back(e);
        // Set initial 3D attributes
        e.Set3DAttributes(mOwner->GetWorldTransform());
    }
    else
    {
        mEvents2D.emplace_back(e);
    }
    return e;
}
```

```cpp
void AudioComponent::OnUpdateWorldTransform()
{
    Matrix4 world = mOwner->GetWorldTransform();
    for (auto& event : mEvents3D)
    {
        if (event.IsValid())
        {
            event.Set3DAttributes(world);
        }
    }
}
```

