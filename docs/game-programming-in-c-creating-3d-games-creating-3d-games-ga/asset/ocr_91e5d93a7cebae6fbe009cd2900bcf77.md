```
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
```