game,” but each asteroid must keep track of neighboring asteroids and handle collisions. A collision typically leads to the destruction of one or more asteroids. Each asteroid must keep a list of other asteroids in its neighborhood. Note that being on such a neighbor list should not keep an asteroid “alive” (so a **shared_ptr** would be inappropriate). On the other hand, an asteroid must not be

# Section 34.3.3 **weak_ptr** 995

destroyed while another asteroid is looking at it (e.g., to calculate the effect of a collision). And obviously, an asteroid destructor must be called to release resources (such as a connection to the graphics system). What we need is a list of asteroids that might still be intact and a way of “grabbing onto one” for a while. A **weak_ptr** does just that:

```
void owner()
{
// …
vector<shared_ptr<Asteroid>> va(100);
for (int i=0; i<va.size(); ++i) {
// … calculate neighbors for new asteroid …
va[i].reset(new Asteroid(weak_ptr<Asteroid>(va[neighbor])));
launch(i);
}
// …
}
```

Obviously, I radically simplified “the owner” and gave each new **Asteroid** just one neighbor. The key is that we give the **Asteroid** a **weak_ptr** to that neighbor. The owner keeps a **shared_ptr** to represent the ownership that’s shared whenever an **Asteroid** is looking (but not otherwise). The collision calculation for an **Asteroid** will look something like this:

```
void collision(weak_ptr<Asteroid> p)
{
if (auto q = p.lock()) { // p.lockreturn sshared_ptr to p’s object
// … that Asteroid still existed: calculate …
}
else { // Oops: that Asteroid has already been destroyed
p.reset();
}
}
```

Note that even if a user decides to shut down the game and deletes all **Asteroids** (by destroying the **shared_ptrs** representing ownership), every **Asteroid** that is in the middle of calculating a collision still finishes correctly: after the **p.lock()**, it holds a **shared_ptr** that will not become invalid.

# 34.4 Allocators