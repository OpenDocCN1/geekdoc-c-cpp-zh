Because this program is relatively simple, your actual design process is not too complicated. You will have a sequence of steps: getting input, classifying the category, and producing output. Because all you're doing when classifying the category is outputting to the result, you can do at the same time as you classify the pressure.

A good way to start facing a programming task is to take the pseudocode steps that you know will follow and transform them into comments.

Then, you can go back later and fill in the code with the comments. These comments serve 2 purposes: They provide an outline that you can follow while developing your code and serve as documentation for the code later so that it's clear which parts belong to.

First, you outline your program, putting in the standard information. Inside of main, you will enter your comments what needs to be done—which came from the pseudocode steps.

You now have your program design and can start filling in parts of the program. As you do, you'll want to frequently stop, using comments to make sure it's running as expected.

You can write some short pseudocode to list the various steps you'll need to follow.

# PSEUDOCODE

Blood Pressure Analyzer

+   1 Read in systolic and diastolic blood pressure Category:
2 Compute and Output Category:
  a Check for Elevated blood pressure: 120<=S<=129 and D<80
  b Check for Stage 1 Hypertension: 130<=S<=139 and 80<=D<=89
  c Check for Stage 2 Hypertension: S>=140 or D>=90
  d Check for Danger Zone: S>=180 or D>=120
  e Check for Hypotension: S<=90 or D<=60
  f Say OK if nothing else happens

```
// Program 4_6 - Stage 1: Pseudocode converted to
// Blood Pressure Analyzer
#include <iostream>
using namespace std;

int main() {
  // Check in systolic and diastolic blood pressures
  // Check for Elevated blood pressure:
  120<=S<=129 and D<80
  // Check for Stage 1 Hypertension: 130<=S<=139
  80<=D<=89
  // Check for Stage 2 Hypertension: 180<=S<=140
  120>D>=90
  // Check for Danger Zone: S>=180 or D>=120
  // Check for Hypotension: S<=90 or D<=60
  Say OK if nothing else happens
}
```