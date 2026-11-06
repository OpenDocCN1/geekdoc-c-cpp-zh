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
```

![](bbox=[0.158, 0.613, 0.239, 0.698])

+   16. Why did the test program introduce the variable `cq_pointer` instead of directly calling `quiz[1]->add_choice("Australia", false)`?
+   
+   17. Which of the following statements are legal?
+      a. `ChoiceQuestion q;`
+         `Question a = q;`
+      b. `ChoiceQuestion b = a;`
+      c. `a.add_choice("Yes", true);`
+      d. `b.add_choice("No", false);`
+   
+   18. Which of the following statements are legal?
+      a. `ChoiceQuestion* p = new ChoiceQuestion;`
+      b. `ChoiceQuestion* q = p;`
+      c. `p->add_choice("Yes", true);`
+      d. `q->add_choice("No", false);`