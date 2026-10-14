```
```
return


def statement(self, skill):
    """Prints a generic statement for choosing
       a skill specialty."""
    self.skill = skill
    print "\n", self.skill, "has
          specializations. If you desire to
          specialize in\\
```

```

a field,\nplease choose from the following list.
      Enter -1 if you don't want a\\
specialization.\n"

```
```
#---Equipment access methods------------------

def setEquipment(self, item):
    """Add equipment to character's inventory.
       """
    self.equipment.append(item)


def getEquipment(self):
    """Display equipment in inventory."""
    print self.equipment
```

```

```
```class Marine(Character):
    """Specialization of a basic character with
       MOS and default skills."""


def __init__(self):
    """Initialize Marine specific values."""

    #---Class attributes
    self.marineInit = 0
    #---Rename attributes
    Character.__init__(self)
    self.intel = self.attrib_dict["intel"]
```
```