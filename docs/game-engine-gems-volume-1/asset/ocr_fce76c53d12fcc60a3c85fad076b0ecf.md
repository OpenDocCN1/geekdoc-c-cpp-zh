# 26.2 The Interfaces of the Game State Observer Pattern

In this section, we begin the process of turning the GameState into an "observable" object and create the foundation that will provide the communication path between the GameState and the other modules of your game.

In order for the software in your game engine to treat the GameState as the subject of observation, we need to create an interface that tells the rest of the game's software that GameState can be observed. The IObservable interface shown in Listing 26.2 provides a way to do this. As you can see, there's very little to this interface, as it only defines the two methods Subscribe() and Unsubscribe(). Some implementations of the observer pattern also define a NotifySubscribers() method in the IObservable interface, but since all interface methods must be defined as public, that would allow other software modules to force observation subjects to notify subscribers even if no change has been made. The game state observer pattern allows the GameState class to decide when to notify its subscribers of a change.

# Listing 26.2: The IObservable and INotifiable interfaces.

```
interface IObservable
{
    void Subscribe(INotifiable observer);
    void Unsubscribe(INotifiable observer);
}

interface INotifiable
{
    void ProcessNotification(IObservable subject);
}
```