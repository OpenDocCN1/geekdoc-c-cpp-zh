```
+ "(The captains gun points oddly at your head.) "
+ "Got it? Yes sir!\n");

// location of ship - this just makes it harder to find the
// ship
iAlienShip = ((iAlienShip * iAmmo) / (iTarget + 1)) + 3;

while (iAmmo > 0) { // when ammo runs out the loop ends
Console.WriteLine("\n\n Enter targeting information?");
input = Console.ReadLine();
iTarget = int.Parse(input);

if (iTarget == iAlienShip) {
// if your input equals the ships location
Console.WriteLine("Alien ship hit, the ships been destroyed sir.");
break; // break ends loop
} else if (iTarget > iAlienShip) {
// when input is too high
Console.WriteLine("You missed, try aiming a little lower");
iAmmo--; // ammo-reduces the total ammo by 1
} else {
// when input is to low
Console.WriteLine("You missed, try aiming higher");
iAmmo--; // also reduces ammo by 1
}

// The location of the ship moves with each shot
if (iTarget == 0) {
iTarget = 1;
}
iAlienShip = (iAlienShip * iAmmo) / iTarget;
}

if (iAmmo > 0) // if you have ammo you must have hit the alien
Console.WriteLine("\n Good work soldier, remind me to promote you.");
else // if your out of ammo you can't protect the hall
Console.WriteLine("\n BOOM!!! You're dead.\n");

Console.WriteLine ("\n Game Over\n");

}
}
```