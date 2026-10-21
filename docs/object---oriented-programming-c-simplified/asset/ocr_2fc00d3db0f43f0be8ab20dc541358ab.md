# 722 Object-Oriented Programming C++ Simplified

```
```cpp
{
	cout << "Enter internal marks :";
	cin >> i_marks;
	if(!(i_marks >= 0 && i_marks <= 60))
	{
		cout << "Invalid Marks";
		exit(0);
	}
}
void show_im()
{
	cout << "Internal marks : " << i_marks << endl;
}
};
class External
{
protected :
	int e_marks;
public :
	void input_em()
	{
		cout << "Enter external marks :";
		cin >> e_marks;
		if(!(e_marks >= 0 && e_marks <= 60))
		{
			cout << "Invalid Marks";
			exit(0);
		}
	}
	void show_em()
	{
		cout << "External marks : " << e_marks << endl;
	}
};
class Total : public Internal, public External
{
	int total_marks;
public :
	void input()
	{
		input_im( );
	}
```
```