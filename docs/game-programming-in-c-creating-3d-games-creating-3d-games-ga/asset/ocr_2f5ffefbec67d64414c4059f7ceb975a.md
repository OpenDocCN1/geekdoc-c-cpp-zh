```
}
    }
    return retVal;
}
```

```
void SoundEvent::Set3DAttributes(const Matrix4& world
{
    auto event = mSystem ? mSystem->GetEventInstance(n
    if (event)
    {
        FMOD_3D_ATTRIBUTES attr;
        // Set position, forward, up
        attr.position = VecToFMOD(worldTrans.GetTransla
        // In world transform, first row is forward
        attr.forward = VecToFMOD(worldTrans.GetXAxis())
        // Third row is up
        attr.up = VecToFMOD(worldTrans.GetZAxis()));
        // Set velocity to zero (fix if using Doppler e
        attr.velocity = { 0.0f, 0.0f, 0.0f };
        event->set3DAttributes(&attr);
    }
```