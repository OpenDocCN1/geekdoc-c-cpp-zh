```
```cpp
{
	NextStud = TempPointer;
}

// Given roll number and name, create an object of student node
friend StudentNode GenerateStudentNode(int TempRollNo, string TempName);

/* StudentNode class and all the members of this class are friends of this function.
   Hence, it can access the private members of StudentNode class */
friend class StudentList;

/* So all members of StudentList class can refer to our private members */
};

StudentNode GenerateStudentNode(int TempRollNo, string TempName)
{
	StudentNode TempStudNode;
	TempStudNode.RollNo = TempRollNo;
	TempStudNode.Name = TempName;
	return TempStudNode;
};

class StudentList
{
	StudentNode *First;
	public:
	void InitializeList()
	{
		First = '\0';
	}

	/* Inserting a student node at the end of a linked list after allocating memory */
	void InsertList(int TempRollNo, string TempName)
	{
		StudentNode *NewStudent = new StudentNode;
		NewStudent -> SetStud(TempRollNo, TempName);
		if(!First)
		{
			First = NewStudent;
			/* If there is no other element, that is, first is null; then, this is the first element */
		}
		else
		{
			StudentNode *TempPtr = First;
			while(TempPtr -> NextStud)
			{
				TempPtr = TempPtr->NextStud;
				// Reached the end of the linked list
				TempPtr -> NextStud = NewStudent;
				// Adding an element here
			}
		}
	}

	void DisplayList()
	{
		StudentNode *TempPtr = First;
		while(TempPtr)
		{
			TempPtr -> WriteStud();
		}
	}
```
```