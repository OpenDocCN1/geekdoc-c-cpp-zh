Instead, you need to store the actual objects elsewhere and collect their locations in an array by storing pointers. We will discuss the use of pointers in the next section.

# 10.4.2 Pointers to Base and Derived Classes

To access objects from different classes in a class hierarchy, use pointers. Pointers to the various objects all have the same size—namely, the size of a memory address—even though the objects themselves may have different sizes.

Here is the code to set up the array of pointers (see Figure 6):

```
Question* quiz[2];
quiz[0] = new Question;
quiz[0]->set_text("Who was the inventor of C++?");
quiz[0]->set_answer("Bjarne Stroustrup");
ChoiceQuestion* cq_pointer = new ChoiceQuestion;
cq_pointer->set_text("In which country was the inventor of C++ born?");
cq_pointer->add_choice("Australia", false);
...
quiz[1] = cq_pointer;
```

As the highlighted code shows, you simply define the array to hold pointers, allocate all objects by calling new, and use the -> operator instead of the dot operator.

> A derived-class pointer can be converted to a base-class pointer.

Note that the last assignment assigns a derived-class pointer of type ChoiceQuestion* to a base-class pointer of type Question*. This is perfectly legal. A pointer is the starting address of an object. Because every ChoiceQuestion is a special case of a Question, the starting address of a ChoiceQuestion object is, in particular, the starting address of a Question object. The reverse assignment—from a base-class pointer to a derived-class pointer—is an error.

The code to present all questions is

```
for (int i = 0; i < QUIZZES; i++)
{
    quiz[i]->display();
    cout << "Your answer: ";
    getline(cin, response);
    cout << quiz[i]->check_answer(response) << endl;
}
```

Again, note the use of the -> operator because quiz[i] is a pointer.

![](bbox=[0.329, 0.711, 0.765, 0.902])

**Figure 6** An Array of Pointers Can Store Objects from Different Classes