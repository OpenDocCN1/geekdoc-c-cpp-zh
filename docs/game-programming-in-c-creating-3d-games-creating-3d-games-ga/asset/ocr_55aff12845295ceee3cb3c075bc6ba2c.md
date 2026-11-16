```
```cpp
class InputComponent : public MoveComponent
{
public:
    InputComponent(class Actor* owner);

    void ProcessInput(const uint8_t* keyState) override;

    // Getter/setters for private variables
    // ...

private:
    // The maximum forward/angular speeds
    float mMaxForwardSpeed;
    float mMaxAngularSpeed;

    // Keys for forward/back movement
    int mForwardKey;
    int mBackKey;

    // Keys for angular movement
    int mClockwiseKey;
    int mCounterClockwiseKey;
};
```
```