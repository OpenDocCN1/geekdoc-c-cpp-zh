```
template <typename T>
static Actor* Create(class Game* game, const rapidjson::Value& inObj)
{
    // Dynamically allocate actor of type T
    T* t = new T(game);
    // Call LoadProperties on new actor
    t->LoadProperties(inObj);
    return t;
}
```