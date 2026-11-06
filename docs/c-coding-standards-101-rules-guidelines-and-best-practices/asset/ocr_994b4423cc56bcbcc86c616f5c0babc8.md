# Coding Style

> > *One man’s constant is another man’s variable.*
> >
> > —Alan Perlis

In this section, we tighten our focus from general design issues to issues that arise most often during actual coding.

The rules and guidelines in this section target coding practices that aren’t specific to a particular language area (e.g., functions, classes, or namespaces) but that improve the quality of your code. Many of these idioms are about getting your compiler to help you, including the powerful tool of declarative **const** (Item 15) and internal **#include** guards (Item 24). Others will help you steer clear of land mines (including some outright undefined behavior) that your compiler can’t always check for you, including avoiding macros (Item 16) and uninitialized variables (Item 19). All of them help to make your code more reliable.

Our vote for the most valuable Item in this section goes to Item 14: Prefer compile- and link-time errors to run-time errors.