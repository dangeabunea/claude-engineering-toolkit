Format PR summary and show this info:
- A short phrase illustrating the goal of the PR
- All the file changes grouped by package
- The key decisions that were made and why
- Visual diagram

Keep summary brief and concise. Goal is to assist human reviewer understand the context
for this PR. 

At the end also add an AASCI diagram to help user undestand how the changes are working together. Use activity diagrams or workflow diagrams based on the actual changes. Pick the one that fits better. Try to keep diagram readable and focused on main flows, not implementation detail.

Example:

````
PR Summary:

Changed how taxes are calculated for European countries.

Key changes:
- Some key classes methods
- Some other key classes or methods

Key decisions
- Some key decision

Diagram

<Some aasci diagram>
````