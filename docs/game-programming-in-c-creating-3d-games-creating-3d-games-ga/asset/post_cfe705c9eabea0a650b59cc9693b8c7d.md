
```cpp
class Ship : public Actor
{
public:
    Ship(class Game* game);
    void UpdateActor(float deltaTime) override;
    void ProcessKeyboard(const uint8_t* state);
    float GetRightSpeed() const { return mRightSpeed; }
    float GetDownSpeed() const { return mDownSpeed; }
private:
    float mRightSpeed;
    float mDownSpeed;
};
```

```cpp
AnimSpriteComponent* asc = new AnimSpriteComponent(this);
std::vector<SDL_Texture*> anims = {
    game->GetTexture("Assets/Ship01.png"),
    game->GetTexture("Assets/Ship02.png"),
    game->GetTexture("Assets/Ship03.png"),
    game->GetTexture("Assets/Ship04.png"),
};
asc->SetAnimTextures(anims);
```

```cpp
void Ship::UpdateActor(float deltaTime)
{
    Actor::UpdateActor(deltaTime);
    // Update position based on speeds and delta time
    Vector2 pos = GetPosition();
    pos.x += mRightSpeed * deltaTime;
    pos.y += mDownSpeed * deltaTime;
    // Restrict position to left half of screen
    // ...
    SetPosition(pos);
}
```

```cpp
Vector2 a;
```

```cpp
Vector2 result = 5.0f * a; // Scaled by 5
```

```cpp
Vector2 a;
a.Normalize(); // a is now normalized
```

```cpp
Vector2 a;
Vector2 result = Vector2::Normalize(a);
```

```cpp
Vector3 Actor::GetForward() const
{
    return Vector2(Math::Cos(mRotation), Math::Sin(mRotation));
}
```

```cpp
Vector3 Actor::GetForward() const
{
    // Negate y-component for SDL
    return Vector2(Math::Cos(mRotation), -Math::Sin(mRotation));
}
```

```cpp
// (ship and asteroid are Actors)
Vector2 shipToAsteroid = asteroid->GetPosition() - ship->GetPosition();
shipToAsteroid.Normalize();
// Convert new forward to angle with atan2 (negate y-component for SDL)
float angle = Math::Atan2(-shipToAsteroid.y, shipToAsteroid.x);
ship->SetRotation(angle);
```

```cpp
float dotResult = Vector2::Dot(origForward, newForward);
float angle = Math::Acos(dotResult);
```

```cpp
position += GetForward() * forwardSpeed * deltaTime;
```

```cpp
rotation += angularSpeed * deltaTime;
```

```cpp
class MoveComponent : public Component
{
public:
	// Lower update order to update first
	MoveComponent(class Actor* owner, int updateOrder = 10);

	void Update(float deltaTime) override;

	float GetAngularSpeed() const { return mAngularSpeed; }
	float GetForwardSpeed() const { return mForwardSpeed; }
	void SetAngularSpeed(float speed) { mAngularSpeed = speed; }
	void SetForwardSpeed(float speed) { mForwardSpeed = speed; }

private:
	// Controls rotation (radians/second)
	float mAngularSpeed;
	// Controls forward movement (units/second)
	float mForwardSpeed;
};
```

```cpp
void MoveComponent::Update(float deltaTime)
{
    if (!Math::NearZero(mAngularSpeed))
    {
        float rot = mOwner->GetRotation();
        rot += mAngularSpeed * deltaTime;
        mOwner->SetRotation(rot);
    }

    if (!Math::NearZero(mForwardSpeed))
    {
        Vector2 pos = mOwner->GetPosition();
        pos += mOwner->GetForward() * mForwardSpeed * deltaTime;
        mOwner->SetPosition(pos);
    }
}
```

```cpp
Asteroid::Asteroid(Game* game)
:Actor(game)
{
    // Initialize to random position/orientation
    Vector2 randPos = Random::GetVector(Vector2::Zero,
        Vector2(1024.0f, 768.0f));
    SetPosition(randPos);
    SetRotation(Random::GetFloatRange(0.0f, Math::TwoPi));

    // Create a sprite component, and set texture
    SpriteComponent* sc = new SpriteComponent(this);
    sc->SetTexture(game->GetTexture("Assets/Asteroid.png"));
    // Create a move component, and set a forward speed
    MoveComponent* mc = new MoveComponent(this);
    mc->SetForwardSpeed(150.0f);
}
```

```cpp
const int numAsteroids = 20;
for (int i = 0; i < numAsteroids; i++)
{
    new Asteroid(this);
}
```

```cpp
virtual void ProcessInput(const uint8_t* keyState) {}
```

```cpp
// ProcessInput function called from Game (not overridable)
void ProcessInput(const uint8_t* keyState);
// Any actor-specific input code (overridable)
virtual void ActorInput(const uint8_t* keyState);
```

```cpp
void Actor::ProcessInput(const uint8_t* KeyState)
{
    if (mState == EActive)
    {
        for (auto comp : mComponents)
        {
            comp->ProcessInput(KeyState);
        }
        ActorInput(KeyState);
    }
}
```

```cpp
mUpdatingActors = true;
for (auto actor : mActors)
{
    actor->ProcessInput(keyState);
}
mUpdatingActors = false;
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

```cpp
void InputComponent::ProcessInput(const uint8_t* keyState)
{
    // Calculate forward speed for MoveComponent
    float forwardSpeed = 0.0f;
    if (keyState[forwardKey])
    {
        forwardSpeed += maxForwardSpeed;
    }
    if (keyState[backKey])
    {
        forwardSpeed -= maxForwardSpeed;
    }
    SetForwardSpeed(forwardSpeed);

    // Calculate angular speed for MoveComponent
    float angularSpeed = 0.0f;
    if (keyState[clockwiseKey])
    {
        angularSpeed += maxAngularSpeed;
    }
    if (keyState[counterClockwiseKey])
    {
        angularSpeed -= maxAngularSpeed;
    }
    SetAngularSpeed(angularSpeed);
}
```

```cpp
acceleration = sumOfForces / mass;
```

```cpp
// (Semi-Implicit) Euler Integration
// Update velocity
velocity += acceleration * deltaTime;
// Update position
position += velocity * deltaTime;
```

```cpp
class CircleComponent : public Component
{
public:
    CircleComponent(class Actor* owner);

    void SetRadius(float radius) { mRadius = radius; }
    float GetRadius() const;

    const Vector2& GetCenter() const;

private:
    float mRadius;
};
```

```cpp
bool Intersect(const CircleComponent& a, const CircleComponent& b)
{
    // Calculate distance squared
    Vector2 diff = a.GetCenter() - b.GetCenter();
    float distSq = diff.LengthSq();

    // Calculate sum of radii squared
    float radiiSq = a.GetRadius() + b.GetRadius();
    radiiSq *= radiiSq;

    return distSq <= radiiSq;
}
```

```cpp
mCircle = new CircleComponent(this);
mCircle->SetRadius(40.0f);
```

```cpp
void Laser::UpdateActor(float deltaTime)
{
    // Do you intersect with an asteroid?
    for (auto ast : GetGame()->GetAsteroids())
    {
        if (Intersect(*mCircle, *(ast->GetCircle())))
        {
            // If this laser intersects with an asteroid,
            // set ourselves and the asteroid to dead
            SetState(EDead);
            ast->SetState(EDead);
            break;
        }
    }
}
```

```cpp
void Ship::ActorInput(const uint8_t* keyState)
{
    if (keyState[SDL_SCANCODE_SPACE] && mLaserCooldown <= 0.0f)
    {
        // Create a laser and set its position/rotation to mine
        Laser* laser = new Laser(GetGame());
        laser->SetPosition(GetPosition());
        laser->SetRotation(GetRotation());

        // Reset laser cooldown (half second)
        mLaserCooldown = 0.5f;
    }
}
```

```cpp
void Ship::UpdateActor(float deltaTime)
{
    mLaserCooldown -= deltaTime;
}
```

```cpp
void AIComponent::Update(float deltaTime)
{
    switch (mState)
    {
    case Patrol:
        UpdatePatrol(deltaTime);
        break;
    case Death:
        UpdateDeath(deltaTime);
        break;
    case Attack:
        UpdateAttack(deltaTime);
        break;
    default:
        // Invalid
        break;
    }
}
```

```cpp
void AIComponent::ChangeState(State newState)
{
// Exit current state
// (Use switch to call corresponding Exit function)
// ...

mState = newState;

// Enter current state
// (Use switch to call corresponding Enter function)
// ...
}
```
