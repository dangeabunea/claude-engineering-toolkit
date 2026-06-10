Format PR summary in 2-3 sentences focusing on the changes introduced in the PR and on the main key decisions if any. Do not mention changed files here, they are an implementation detail. 

Keep summary brief and concise. Goal is to assist human reviewer understand the context
for this PR. 

Example:

````
PR Summary:

Changed how taxes are calculated for European countries. Added DB configuration rows for each country that includes national taxes and used them in computations instead of hardcoded values. They need to be saved in DB so editing is easier. 
````