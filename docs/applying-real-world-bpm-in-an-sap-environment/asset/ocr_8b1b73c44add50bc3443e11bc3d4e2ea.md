rules may handle the interaction, display different questions, and adapt the user interface to gather the required data.

Good decision service design requires a clear understanding of what is needed from a requirements perspective and what is plausible from an architectural and technical perspective. Option 1 is the cleanest and most common but can be limiting when large amounts of optional data are involved. Options 2 to 4 provide more flexibility but increase the challenges: The number of failure points increases, which can be crippling if not managed well; the complexity can rapidly increase because of maintenance, monitoring, and error-handling needs; and more resources must be dedicated to manage the additional integration points in the infrastructure.

# Business Rules Management

Most organizations adopting business rules find that different rulesets require different types of business rules management. Sometimes business people change the business rules in production, sometimes business people make changes to business rules in a development environment, sometimes business analysts or IT staff make changes, and so on. SAP's business rules offerings support a variety of editing approaches designed for both business and IT users and the necessary access controls as described in Section 14.4.4.

Whereas there are pros and cons for each approach, it is important to remember that, fundamentally, the value of business rules and of business rules management system lies in collaboration. It matters less who makes the changes than who can collaborate to ensure that the right change is made at the right time.

SAP's business rules syntax allows for flexibility and power not available in traditional programming languages. This lets business policymakers work side by side with the implementation team, reading and discussing the business rules directly. This is true regardless of the approach taken to business rules management.

Several distinct choices must be made for each ruleset:

+   - Who should be able to make changes to the rules?
+   - How quickly do those changes need to get into production?
+   - How rigorous does checking and testing need to be before the changes go into production?

Each ruleset can have different answers, though many rulesets have the same set of answers and can be treated the same way. You should not, however, assume