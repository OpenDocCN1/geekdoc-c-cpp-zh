```
void Actor::SaveProperties(rapidjson::Document::AllocatorType& alloc,
        rapidjson::Value& inObj) const
{
    std::string state = "active";
    if (mState == EPaused)
    {
        state = "paused";
    }
    else if (mState == EDead)
    {
        state = "dead";
    }

    JsonHelper::AddString(alloc, inObj, "state", state);
    JsonHelper::AddVector3(alloc, inObj, "position", mPosition);
    JsonHelper::AddQuaternion(alloc, inObj, "rotation", mRotation);
    JsonHelper::AddFloat(alloc, inObj, "scale", mScale);
}
```