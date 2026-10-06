# Elevators in a Building

Design an elevator system for the following building:

+   * 100 floors in the building
* 3 total occupants
  * Occupant 1 is a company that occupies the top 10 floors.
  * Occupant 2 is a company that occupies 45 floors below occupant 1.
  * Occupant 3 is a company that occupies 45 floors below occupant 2.

Things to Consider

+   * Interviewer is looking for a logical and thoughtful elevator allocation.
* Clarify assumptions upfront such as population, peak hours and average load.
* Forgetting that some elevators should be reserved for maintenance teams or emergency responders.

Common Mistakes

# Answer

CANDIDATE: I'm guessing you want the overall percentage allocation, not the actual number of elevators for the building right?

INTERVIEWER: That's correct.

CANDIDATE: Do you have information about the number of people on each floor?

INTERVIEWER: Assume that every floor has the same number of occupants.

CANDIDATE: Should I worry that the elevators are too small or won't function properly if it's too heavy?

INTERVIEWER: Let's say that the size of the elevator and the acceptable weight load is not part of this problem.

CANDIDATE: What are the peak hours of usage?

INTERVIEWER: Since we're short on time, let's not worry about the peak hours of usage. Can you wrap your answer in the next to two minutes?

CANDIDATE: Sure, give me a moment to digest the information I know so far, and I'll be prepared to give you your recommendation.

Candidate takes one minute.

The obvious thing to do is allocate 10% of the elevators to occupant 1 and then 45% each to occupants 2 and 3. However, this assumes that current occupant configuration will stay fixed. We cannot assume this. Corporate tenants come and go.