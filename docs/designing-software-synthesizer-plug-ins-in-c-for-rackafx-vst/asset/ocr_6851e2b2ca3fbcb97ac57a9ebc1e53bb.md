```
void AUSynth::update()
{
    <SNIP SNIP SNIP>

    // --- update EG
m_EG1.setAttackTime_msec(Globals())->GetParameter(EG1_ATTACK_MSEC);
m_EG1.setDecayTime_msec(Globals())->GetParameter(EG1_DECAY_MSEC);
m_EG1.setSustainLevel(Globals())->GetParameter(EG1_SUSTAIN_LEVEL);
m_EG1.setReleaseTime_msec(Globals())->GetParameter(EG1_RELEASE_MSEC);
m_EG1.m_bResetToZero = Globals()->GetParameter(RESET_TO_ZERO);
m_EG1.m_bLegatoMode = Globals()->GetParameter(LEGATO_MODE);

    // --- update DCA
m_DCA.setPanControl(Globals())->GetParameter(OUTPUT_PAN);
m_DCA.setAmplitude_dB(Globals())->GetParameter(OUTPUT_AMPLITUDE_DB);
m_DCA.update();
}
```