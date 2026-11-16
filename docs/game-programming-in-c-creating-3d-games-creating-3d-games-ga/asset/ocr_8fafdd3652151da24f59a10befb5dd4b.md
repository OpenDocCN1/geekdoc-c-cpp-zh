```
void MeshComponent::LoadProperties(const rapidjson::Value& inObj)
{
    Component::LoadProperties(inObj);

    std::string meshFile;
    if (JsonHelper::GetString(inObj, "meshFile", meshFile))
        SetMesh(mOwner->GetGame()->GetRenderer()->GetMesh(meshFile));
    }

    int idx;
    if (JsonHelper::GetInt(inObj, "textureIndex", idx))
    {
        mTextureIndex = static_cast<size_t>(idx);
    }

    JsonHelper::GetBool(inObj, "visible", mVisible);
    JsonHelper::GetBool(inObj, "isSkeletal", mIsSkeletal);
}
```