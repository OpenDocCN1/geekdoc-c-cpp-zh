
*In the same way that vehicles can differ in their method of locomotion, polymorphic objects carry out tasks in different ways.*

![](img/23fb3582e93ebc95909e1de029c3d388_486_0.png)

### 10.4.4 Polymorphism

Polymorphism (literally, “having multiple shapes”) describes objects that share a set of tasks and execute them in different ways.

The quiz array collects a mixture of both kinds of questions. Such a collection is called **polymorphic** (literally, “of multiple shapes”). Objects in a polymorphic collection have some commonality but are not necessarily of the same type. Inheritance is used to express this commonality, and virtual functions enable variations in behavior.

Virtual functions give programs a great deal of flexibility. The question presentation loop describes only the general mechanism: “Display the question, get a response, and check it.” Each object knows on its own how to carry out the specific tasks: “Display the question” and “Check a response.”

Using virtual functions makes programs easily extensible. Suppose we want to have a new kind of question for calculations, where we are willing to accept an approximate answer. All we need to do is to define a new class `NumericQuestion`, with its own `check_answer` function. Then we can populate the quiz array with a mixture of plain questions, choice questions, and numeric questions. The code that presents the questions need not be changed at all! The calls to the virtual functions automatically select the correct member functions of the newly defined classes.

Here is the final version of the quiz program, using pointers and virtual functions. When you run the program, you will find that the appropriate versions of the virtual functions are called. (The files `question.cpp` and `choicequestion.cpp` are included in your book’s companion code.)

`ch10/quiz3/question.h`

```cpp
#ifndef QUESTION_H
#define QUESTION_H

#include <string>

using namespace std;

class Question
{
public:
   /**
    * Constructs a question with empty question and answer.
    */
   Question();

   /*
    * @param question_text the text of this question
    */
   void set_text(string question_text);

   /*
    * @param correct_response the answer for this question
    */
   void set_answer(string correct_response);

   /*
    * @param response the response to check
    * @return true if the response was correct, false otherwise
    */
   virtual bool check_answer(string response) const;

   /*
    * Displays this question.
    */
   virtual void display() const;
private:
    string text;
    string answer;
};
#endif
```

`ch10/quiz3/choicequestion.h`

```cpp
#ifndef CHOICEQUESTION_H
#define CHOICEQUESTION_H

#include <vector>
#include "question.h"

class ChoiceQuestion : public Question
{
public:
    /*
     * Constructs a choice question with no choices.
     */
    ChoiceQuestion();

    /*
     * Adds an answer choice to this question.
     * @param choice the choice to add
     * @param correct true if this is the correct choice, false otherwise
     */
    void add_choice(string choice, bool correct);

    virtual void display() const;
private:
    vector<string> choices;
};

#endif
```

```cpp
#include <iostream>
#include "question.h"
#include "choicequestion.h"

int main()
{
   string response;
   cout << boolalpha;

   // Make a quiz with two questions
   const int QUIZZES = 2;
   Question* quiz[QUIZZES];
   quiz[0] = new Question;
   quiz[0]->set_text("Who was the inventor of C++?");
   quiz[0]->set_answer("Bjarne Stroustrup");

   ChoiceQuestion* cq_pointer = new ChoiceQuestion;
   cq_pointer->set_text(
      "In which country was the inventor of C++ born?");
   cq_pointer->add_choice("Australia", false);
   cq_pointer->add_choice("Denmark", true);
   cq_pointer->add_choice("Korea", false);
   cq_pointer->add_choice("United States", false);
   quiz[1] = cq_pointer;

   // Check answers for all questions
   for (int i = 0; i < QUIZZES; i++)
   {
      quiz[i]->display();
      cout << "Your answer: ";
      getline(cin, response);
      cout << quiz[i]->check_answer(response) << endl;
   }

   return 0;
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_488_0.png)

- 16. Why did the test program introduce the variable `cq_pointer` instead of directly calling `quiz[1]->add_choice("Australia", false)`?
- 17. Which of the following statements are legal?
  - a. `ChoiceQuestion q;`
    `Question a = q;`
  - b. `ChoiceQuestion b = a;`
  - c. `a.add_choice("Yes", true);`
  - d. `b.add_choice("No", false);`
- 18. Which of the following statements are legal?
  - a. `ChoiceQuestion* p = new ChoiceQuestion;`
  - b. `ChoiceQuestion* q = p;`
  - c. `p->add_choice("Yes", true);`
  - d. `q->add_choice("No", false);`
- 19. What is displayed as the result of the following statements?

```cpp
ChoiceQuestion* p = new ChoiceQuestion();
p->set_text("What is the answer?");
p->add_choice("42", true);
p->add_choice("Something else", false);
Question q = *p;
q.display();
```

- 20. Suppose check_answer was not declared virtual in question.h. How would the behavior of test.cpp change?

**Practice It** Now you can try these exercises at the end of the chapter: R10.14, R10.15, P10.11, P10.12.

## Programming Tip 10.2

### Don't Use Type Tags

![](img/23fb3582e93ebc95909e1de029c3d388_489_0.png)

Some programmers build inheritance hierarchies in which each object has a tag that indicates its type, commonly a string. They then query that string:

```cpp
if (q->get_type() == "Question")
{
   // Do something
}
else if (q->get_type() == "ChoiceQuestion")
{
   // Do something else
}
```

This is a poor strategy. If a new class is added, then all these queries need to be revised. In contrast, consider the addition of a class *NumericQuestion* to our quiz program. *Nothing* needs to change in that program because it uses virtual functions, not type tags. Whenever you find yourself adding a type tag to a hierarchy of classes, reconsider and use virtual functions instead.

## Common Error 10.4

### Slicing an Object

![](img/23fb3582e93ebc95909e1de029c3d388_489_1.png)

In C++ it is legal to copy a derived-class object into a base-class variable. However, any derived-class information is lost in the process. For example, when a Manager object is assigned to a variable of type Employee, the result is only the employee portion of the manager data:

```cpp
Manager m;

Employee e = m; // Holds only the Employee base data of m
```

Any information that is particular to managers is sliced off, because it would not fit into a variable of type Employee. To avoid slicing, you can use pointers.

The slicing problem commonly occurs when a function has a polymorphic parameter (that is, a parameter that can belong to a base class or a derived class). In that case, the parameter variable must be a pointer or a reference. Consider this example:

```cpp
void ask(Question q) // Error
{
    q.display();
    cout << "Your answer: ";
    getline(cin, response);
    cout << q.check_answer(response) << endl;
}
```

If you call this function with a ChoiceQuestion object, then the parameter variable q is initialized with a copy of that object. But q is a Question object; the derived-class information is sliced away. The simplest remedy is to use a reference:

```cpp
void ask(const Question& q)
```

Now only the address is passed to the function. A reference is really a pointer in disguise. No slicing occurs, and virtual functions work correctly.

## Special Topic 10.2

![](img/23fb3582e93ebc95909e1de029c3d388_490_0.png)

### Virtual Self-Calls

Suppose we add the following function to the Question class:

```cpp
void Question::ask() const
{
    display();
    cout << "Your answer: ";
    getline(cin, response);
    cout << check_answer(response) << endl;
}
```

Now consider the call

```cpp
ChoiceQuestion cq;
cq.set_text("In which country was the inventor of C++ born?");
...
cq.ask();
```

Which display and check_answer function will the ask function call? If you look inside the code of the Question::ask function, you can see that these functions are executed on the implicit parameter:

```cpp
void Question::ask() const
{
    implicit_parameter.display();
    cout << "Your answer: ";
    getline(cin, response);
    cout << implicit_parameter.check_answer(response) << endl;
}
```

The implicit parameter in our call is cq, an object of type ChoiceQuestion. Because the display and check_answer functions are virtual, the ChoiceQuestion versions of the functions are called automatically. This happens even though the ask function is defined in the Question class, which has no knowledge of the ChoiceQuestion class.

As you can see, virtual functions are a very powerful mechanism. The Question class supplies an ask function that specifies the common nature of asking a question, namely to display it and check the response. How the displaying and checking are carried out is left to the derived classes.
