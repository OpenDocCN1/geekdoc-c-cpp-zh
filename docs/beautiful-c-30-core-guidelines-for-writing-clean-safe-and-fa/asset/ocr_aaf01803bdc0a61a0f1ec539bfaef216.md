member functions add nothing to the class. This is precisely what the guideline is telling you not to do.

Try this example:

Click here to view code image

```
class team
{
public:
    void add_player(std::string name) {
        if (players_.size() < 11)
players_.push_back(name); }
    std::vector<string> get_players() const {
        return players_; }

private:
    std::vector<string> players_;
}
```

The class invariant is that a team can have no more than 11 players.

Access levels allow a class designer to easily preserve class invariants by checking the effect of operations on the member data and ensuring that all the data retains valid values.

This guideline gives as its reason “A trivial getter or setter adds no semantic value; the data item could just as well be public.” As we can see from the house example and the point example, that is exactly the case. There is no semantic difference between struct house and class house. The member functions in class point are redundant. There is an operational difference in that there is an opportunity to set breakpoints where the member data is read and written, but that has no impact on the semantic nature of the house abstraction or the point abstraction.

When creating a class and designing its interface it is quite usual to think of aspects of the abstraction being modeled with numbers: this is a computer you’re writing for, after all. The temptation becomes simply to make those aspects numeri-cal data members. If a client wants to change something, they call the function to set the new value and, after some