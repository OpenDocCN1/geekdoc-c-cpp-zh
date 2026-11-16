```
CLIPS> (watch activations)._
CLIPS> (reset)._
==> Activation 0      all-fires-being-handled:
    f-0,
CLIPS>
```

Once an emergency fact is asserted, the rule is deactivated until the appropriate fire-squad and evacuated facts are asserted:

```
CLIPS>
(assert (emergency (type fire)
        (location building-11)))_
==> Activation 0      all-fires-being-handled: f-0,
<Fact-1>
CLIPS>
(assert (evacuated (building building-11)))_
<Fact-2>
CLIPS>
(assert (fire-squad (name A)
        (location building-11)))_
==> Activation 0      all-fires-being-handled: f-0,
<Fact-3>
CLIPS>
(assert (fire-squad (name B)
        (location building-1)))_
<Fact-4>
CLIPS>
(assert (emergency (type fire)
        (location building-1)))_
==> Activation 0      all-fires-being-handled: f-0,
<Fact-5>
CLIPS> (assert (evacuated (building building-1)))_
==> Activation 0      all-fires-being-handled:
f-0,
<Fact-6>
CLIPS>
```

If the fire-squad fact for building-1 is removed, then the rule is deactivated. Removing the emergency fact for this building will reactivate the rule:

```
CLIPS> (retract 4)._
==> Activation 0      all-fires-being-handled: f-0,
CLIPS> (retract 5)._
==> Activation 0      all-fires-being-handled: f-0,
CLIPS> (run)._
All buildings that are on fire
have been evacuated and
```