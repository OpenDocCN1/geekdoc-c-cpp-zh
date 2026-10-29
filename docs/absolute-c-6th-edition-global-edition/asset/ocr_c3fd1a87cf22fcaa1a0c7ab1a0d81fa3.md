An implementation of getDamage( ) is given here:

```
int Creature::getDamage()
{
    int damage;
    // All creatures inflict damage, which is a
    // random number up to their strength
    damage = (rand() % strength) + 1;
    cout << getSpecies() << " attacks for " <<
        damage << " points!" << endl;

    // Demons can inflict damage of 50 with a 5% chance
    if ((type == 2) || (type == 1))
        if ((rand() % 100) < 5)
        {
            damage = damage + 50;
            cout << "Demonic attack inflicts 50 "
                << "additional damage points!" << endl;
        }

    // Elves inflict double magical damage with a 10% chance
    if (type == 3)
    {
        if ((rand() % 10)==0)
        {
            cout << "Magical attack inflicts " << damage<<
                "additional damage points!" << endl;
            damage = damage * 2;
        }
    }

    // Balrogs are so fast they get to attack twice
    if (type == 2)
    {
        int damage2 = (rand() % strength) + 1;
        cout << "Balrog speed attack inflicts " << damage2 <<
            "additional damage points!" << endl;
        damage = damage + damage2;
    }
    return damage;
}
```

One problem with this implementation is that it is unwieldy to add new creatures. Rewrite the class to use inheritance, which will eliminate the need for the variable type. The Creature class should be the base class. The classes Demon, Elf, and Human should be derived from Creature. The classes Cyberdemon and Balrog