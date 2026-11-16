
event, after defining a state machine, the next step is to
implement it in code.

## Basic State Machine Implementation

There are several ways to implement a state machine.
Minimally, the code must update the behavior of the
AI based on the current state, and it must support
enter and exit actions. An `AIComponent` class can
encapsulate this state behavior.

If there are only two states, a simple Boolean check in
`Update` would work, though it isn't very robust. A more
flexible implementation is to use an enum to represent
the different states. For the state machine in Figure 4.1,
this is the enum declaration:

```
enum AIState
{
    Patrol,
    Death,
    Attack
};
```

Then, you create an `AIComponent` class that has an
instance of `AIState` as member data. You also define
separate update functions for each state:
`UpdatePatrol`, `UpdateDeath`, and `UpdateAttack`.

The `AIComponent::Update` function then has a switch on the `AIState` member variable and calls the update function that corresponds to the current state:

Click here to view code image

```
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

You can handle the state machine transitions in a separate `ChangeState` function. This way, the various update functions can initiate a transition just by calling `ChangeState`. You can implement `ChangeState` as follows:

Click here to view code image

```
void AIComponent::ChangeState(State newState)
{
    // Exit current state
    // (Use switch to call corresponding Exit function
    // ...

    mState = newState;

    // Enter current state
    // (Use switch to call corresponding Enter function
    // ...
}
```

Although this implementation is simple, there are issues.

First, it doesn't scale well; adding more states reduces the readability of both `Update` and `ChangeState`. Also, having so many separate `Update`, `Enter`, and `Exit` functions also makes the code harder to follow.

It's also not easy to mix and match functionality between multiple AIs. Two different AIs with different state machines need separate enums and, therefore, separate AI components. But many AI characters may share some functionality. Suppose two AIs have mostly different state machines, but both have a Patrol state. With this basic implementation, it isn't easy to share the Patrol code between both AI components.

## States as Classes

An alternative approach to the one just described is to use classes to represent each state. First, define a base class for all states called `AIState`:

Click here to view code image

```cpp
class AIState
{
public:
    AIState(class AIComponent* owner)
    :mOwner(owner)
    { }

    // State-specific behavior
    virtual void Update(float deltaTime) = 0;

    virtual void OnEnter() = 0;

    virtual void OnExit() = 0;

    // Getter for string name of state
    virtual const char* GetName() const = 0;

protected:
    class AIComponent* mOwner;
};
```

The base class includes several virtual functions to control the state: Update updates the state, OnEnter implements any entry transition code, and OnExit implements any exit transition code. The GetName function simply returns a human-readable name for the state. You also associate AIState with a specific AIComponent through the mOwner member variable.

Next, declare the AIComponent class, as follows:

Click here to view code image

```
class AIComponent : public Component
{
public:
    AIComponent(class Actor* owner);
    void Update(float deltaTime) override;
    void ChangeState(const std::string& name);

    // Add a new state to the map
    void RegisterState(class AIState* state);
private:
    // Maps name of state to AIState instance
    std::unordered_map<std::string, class AIState*> mStateMap;
    // Current state we're in
    class AIState* mCurrentState;
};
```

Notice how AIComponent has a hash map of state names to AIState instance pointers. It also has a pointer to the current AIState. The RegisterState function takes in a pointer to an AIState and adds the state to the map:

Click here to view code image

```
void AIComponent::RegisterState(AIState* state)
{
    mStateMap.emplace(state->GetName(), state);
}
```

The `AIComponent::Update` function is also straightforward. It simply calls `Update` on the current state, if it exists:

Click here to view code image

```
void AIComponent::Update(float deltaTime)
{
    if (mCurrentState)
    {
        mCurrentState->Update(deltaTime);
    }
}
```

However, the `ChangeState` function does several things, as shown in Listing 4.1. First, it calls `OnExit` on the current state. Next, it tries to find the state you're changing to in the map. If it finds this state, it changes `mCurrentState` to the new state and calls `OnEnter` on this new state. If it can't find the next state in the map, it outputs an error message and sets `mCurrentState` to `null`.

### Listing 4.1 AIComponent::ChangeState Implementation

Click here to view code image

```
void AIComponent::ChangeState(const std::string& name)
{
    // First exit the current state
    if (mCurrentState)
    {
        mCurrentState->OnExit();
    }

    // Try to find the new state from the map
    auto iter = mStateMap.find(name);
    if (iter != mStateMap.end())
    {
        mCurrentState = iter->second;
        // We're entering the new state
        mCurrentState->OnEnter();
    }
    else
    {
        SDL_Log("Could not find AIState %s in state map");
        mCurrentState = nullptr;
    }
}
```

You can use this pattern by first declaring subclasses of AIState, like this AIPatrol class:

Click here to view code image

```cpp
class AIPatrol : public AIState
{

public:
    AIPatrol(class AIComponent* owner);

    // Override with behaviors for this state
    void Update(float deltaTime) override;

    void OnEnter() override;

    void OnExit() override;

    const char* GetName() const override
    { return "Patrol"; }
};
```

You then implement any special behaviors in Update, OnEnter, and OnExit. Suppose you want AIPatrol to change to the AIDeath state when the character dies. To initiate the transition, you need to call ChangeState on the owning component, passing in the name of the new state:

Click here to view code image

```cpp
void AIPatrol::Update(float deltaTime)
{
    // Do some other updating
    // ...
    bool dead = /* Figure out if I'm dead */;
    if (dead)
    {
        // Tell the ai component to change states
        mOwner->ChangeState("Death");
    }
}
```

On the ChangeState call, the AIComponent looks into its state map, and if it finds a state named Death, it transitions into this state. You can similarly declare AIDeath and AIAttack classes to complete the basic state machine from Figure 4.1.

To hook up the states into an AIComponent's state map, first create an actor and its AIComponent and then call Register on any states you wish to add to the state machine:

Click here to view code image

```
Actor* a = new Actor(this);

// Make an AIComponent

AIComponent* aic = new AIComponent(a);

// Register states with AIComponent

aic->RegisterState(new AIPatrol(aic));
aic->RegisterState(new AIDeath(aic));
aic->RegisterState(new AIAttack(aic));
```

To then set the AIComponent to an initial patrol state, you call ChangeState, as follows:

```
aic->ChangeState("Patrol");
```

Overall, this approach is useful because each state's implementation is in a separate subclass, which means the AIComponent remains simple. It also makes it significantly easier to reuse the same states for different AI characters. You simply need to register whichever states you want with the new actor's AIComponent.

## PATHFINDING

A **pathfinding** algorithm finds a path between two points, avoiding any obstacles in the way. The complexity of this problem stems from the fact that there might be a large set of paths between two points, but only a small number of these paths are the shortest. For example, Figure 4.3 shows two potential routes between points A and B. An AI traveling along the solid path is not particularly intelligent because the dashed path is shorter. Thus, you need a method to efficiently search through all the possible paths to find one with the shortest distance.

![](img/e9afcec1487716b0ef80d7e7c09869c8_245_0.png)

**Figure 4.3** Two paths from A to B

## Graphs

Before you can solve the pathfinding problem, you first need a way to represent the parts of the game
