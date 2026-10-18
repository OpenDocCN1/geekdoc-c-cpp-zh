for your C++ compiler or check with a friend who has a similar computer setup. The necessary change is undoubtedly very small and, once you find out what it is, very easy.

# SELF-TEST EXERCISES

16. If the following statement were used in a C++ program, what would it cause to be written on the screen?

```
cout << "C++ is easy to understand.";
```

17. What is the meaning of \n as used in the following statement (which appears in Display 1.8)?

```
cout << "Enter the number of peas in a pod:\n";
```

18. What is the meaning of the following statement (which appears in Display 1.8)?

```
cin >> peasPerPod;
```

19. What is the meaning of the following statement (which appears in Display 1.8)?

```
totalPeas = numberOfPods * peasPerPod;
```

20. What is the meaning of this directive?

```
#include <iostream>
```

21. What, if anything, is wrong with the following #include directives?

+   a. #include <iostream >
+   b. #include < iostream>
+   c. #include <iostream>

# 1.4 TESTING AND DEBUGGING

> "And if you take one from three hundred and sixty-five, what remains?"
> "Three hundred and sixty-four, of course."
> Humpty Dumpty looked doubtful. "I'd rather see that done on paper," he said.
> LEWIS CARROLL, Through the Looking-Glass

A mistake in a program is usually called a bug, and the process of eliminating bugs is called debugging. There is colorful history of how this term came into use. It occurred in the early days of computers, when computer hardware was