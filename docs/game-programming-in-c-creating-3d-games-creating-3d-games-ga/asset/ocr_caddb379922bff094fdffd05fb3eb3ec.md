```
float mAngularSpeed;

// Controls forward movement (units/second)
float mForwardSpeed;

};
```

The implementation of Update, shown in Listing 3.2, simply converts the movement pseudocode into actual code. Recall that a Component class can access its owning actor through the mOwner member variable. You use this mOwner pointer to then access the position, rotation, and forward of the owning actor. Also note the use of the Math::NearZero function here. This function compares the absolute value of the parameter with some small epsilon amount to determine whether the value is “near” zero. In this specific case, you don’t bother updating the rotation or position of the actor if the corresponding speed is near zero.

# Listing 3.2 MoveComponent::Update Implementation

Click here to view code image

```
void MoveComponent::Update(float deltaTime)
{
if (!Math::NearZero(mAngularSpeed))
{
```