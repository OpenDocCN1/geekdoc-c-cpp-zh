# **LISTING 4-5:** *(continued)*

```
    void Engine::Stop() {
      RPM = 0;
      Revamount = 0;
      Changed();
    }

    void Electric::ChangeOutputBy(int amount) {
      Output += amount;
      ChangedBy = amount;
      Changed();
    }

    void Wheels::Accelerate(int amount) {
      Speed += amount;
      Changed();
    }

    void Wheels::Decelerate(int amount) {
      Speed -= amount;
      Changed();
    }

    void Brakes::Apply(int amount) {
      Pressure = amount;
      Changed();
    }

    void Headlights::Adjust(int Amount) {
      Brightness += Amount;
    }

    void AirConditioner::TurnOn() {
      ChangedBy = 100 - Level;
      Level = 100;
      Changed();
    }

    void AirConditioner::TurnOff() {
      ChangedBy = 0 - Level;
      Level = 0;
      Changed();
    }
```