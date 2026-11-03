# Algorithm

Start
**Step 1:** Input x
**Step 2:** Initialize i←1, sum←0, term←1, fact←1
**Step 3:** While term >= FLT_EPSILON
  fact ← fact*i
  sum ← sum+term
  term ← pow(x, i)/fact
  Increment i by 1
**Step 4:** Output the calculated value
**Step 5:** Output Library function value
Stop