# Controlling It All: The menuManager Class

The menuManager class is the real workhorse of the menuing system, as its description hinted earlier. Implemented as a singleton, the menuManager ensures that only one instance is ever created, providing a single control center for creating and rendering menus as well as tracking the user’s path through the system. The menuManager consists of two main pieces, the manager itself and the menu factory.

# The Manager

Depending on the game, the amount of menus can become unwieldy very quickly; the menu manager keeps this in check. The manager accomplishes this by keeping a list of all the menus the user has already visited. The last menu in this list is seen as the current menu. When updating or rendering a menu, the manager simply accesses the last object in the list and passes on the command.

The list of menus, known as the menu trail, is how the menu manager tracks which menus the user has visited. At times, there may be multiple pathways that lead to a single menu, making it difficult to return the user to the correct previous screen. The menu trail solves this problem. If the user wants to backtrack through the menus, the manager need only traverse the menu trail in reverse.

We have only discussed how the menu manager uses the menus in the trail so far; in the next section, we will cover how the menus are created. Listing 1.17.3 shows the menuManager class.

# Listing 1.17.3 The menuManager Class

```
class menuManager
{
public:
    // singleton to ensure only one instance of the
    // menu system
    static menuManager& getInstance()
    {
        if (pInstance == NULL) pInstance = new menuManager();
        return *pInstance;
    };

    // initialize the menu system
    bool init(void);

    // close and release the menu system
    void shutdown(void);

    // passes down update messages to the menus
    int update(BYTE keys[]);

    // draws the menus
    void render(void);
```