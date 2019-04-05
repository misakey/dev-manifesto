# Coding style 

We want to produce a code that is consistent between projects and developers. 
So we follow linting rules for each language we use.
No code should be written (or at least merged) that don't follow those rules. 
(we need to create a CI to enforce that).

## Clean code

We have an inspiration on the Clean Code (from Robert C. Martin).
Some rules we use specifically:

### The boyscout rule

"Leave your code(campground) better than you found it."

### Explicit / searchable naming

The name of the functions, the objects, the interfaces (and the variables) should be explicit, understandable and searchable (avoid `a`, `i`, ...), to mitigate with the idioms of the tech you are using.

# Language specific

## Javascript / React

We use ESLint.
The linting rules we follow are based on Airbnb's rules.
We just add some modifications:
* `"react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }]`: we use `.js` files
* `"react/forbid-prop-types": [1, { "forbid": ["any", "array"] }]`: accept most of the proptypes. Just no "any" or "array" (use arrayOf instead)
* `"import/prefer-default-export": false`: we prefer default exports, but for some tools files (for example) we need to allow multiple exports

You can find an `.eslintrc.json` file in the resources folder.
These rules should be used in **every** project. 
If you want to modify the ruleset we use, you can open a pull request on this project with the `.eslintrc.json` file updated and this file updated with explanation of what was changed. It'll be reviewed by all the frontend team and if accepted applied to all projects.

## Python

TODO
Misc ideas:
* pylint and pep rules
* enforce black ? Or not ?

## Golang

TODO