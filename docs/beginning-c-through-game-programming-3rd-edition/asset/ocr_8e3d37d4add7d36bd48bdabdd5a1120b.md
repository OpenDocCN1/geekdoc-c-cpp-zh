# The Player class

The Player class represents a human player. It’s derived from GenericPlayer.

```
```cpp
class Player : public GenericPlayer
{
public:
	Player(const string& name = "");
	virtual ~Player();

	virtual bool IsHitting() const;

	//announces that the player wins
	void Win() const;

	//announces that the player loses
	void Lose() const;

	//announces that the player pushes
	void Push() const;
};

Player::Player(const string& name):
	GenericPlayer(name)
{}

Player::~Player()
{}

bool Player::IsHitting() const
{
	cout << m_Name << ", do you want a hit? (Y/N): ";
	char response;
	cin >> response;
	return (response == 'y' || response == 'Y');
}

void Player::Win() const
{
	cout << m_Name << " wins.\n";
}
```
```