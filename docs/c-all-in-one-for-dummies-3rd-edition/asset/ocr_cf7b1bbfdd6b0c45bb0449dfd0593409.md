# Listing 6-4 (continued)

```
```cpp
void Engine::PushGasPedal(int amount)
{
    Revamount = amount;
    RPM += Revamount;
    Changed();
}

void Engine::ReleaseGasPedal(int amount)
{
    Revamount = amount;
    RPM -= Revamount;
    Changed();
}

void Engine::Stop()
{
    RPM = 0;
    Revamount = 0;
    Changed();
}

void Electric::ChangeOutputBy(int amount)
{
    Output += amount;
    ChangedBy = amount;
    Changed();
}

void Wheels::Accelerate(int amount)
{
    Speed += amount;
    Changed();
}

void Wheels::Decelerate(int amount)
{
    Speed -= amount;
    Changed();
}

void Brakes::Apply(int amount)
{
    Pressure += amount;
    Changed();
}

void Headlights::Adjust(int Amount)
{
    Brightness += Amount;
}
```
```