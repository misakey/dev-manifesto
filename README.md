# Conventions applied to Misakey development

## Coding style / Linting

### Javascript / React

For javascript / React project, we use ESLint with the AirBnB's rules. 
Some rules have been disabled / tweaked for our own needs, you can see them in the `src/frontend/.eslintrc.json`.

Any modification of the rules (and so to this file) should be discussed and approved by all the core team.

Any contribution should reflect the ESLint rules, so we recommand you to install an ESLint addon to your IDE.

**Todo:** Adding a pipline to test the Linting, and automatically block a merge request if Linting is incorrect.

### Python

**Todo:** The Pylint configuration should be rethinked, and applied. We tried to use Black, but we're currently not sure to use it at end. 
It's a WIP to structurate this well. 

### GO

**TODO**

## GIT conventions

### Branches

We are using **[git flow](https://nvie.com/img/git-model@2x.png)**, we advise you're using the [git flow CLI](https://danielkummer.github.io/git-flow-cheatsheet/)

So as branches we have:
- **master**: Last stable release (what is in production)
- **develop**: Theorically stable branch, with new features (waiting to be fully tested / released)
- **feature/++**: Features branches (merge to develop)
- **bugfix/++**: Bugfix branches (merge to develop)
- **hotfix/++**: Hotfix branches (merge to master & develop)
- **release/++**: Release branches (merge to master & develop)

On top of git flow:
- We're adding the issue ID linked to the feature (or the hotfix if existing), before the name of the feature (or the hotfix).
- Branches are named lowercase, with dash between words

#### Examples

##### Using the gitflow CLI

Starting a feature: `git flow feature start 14-reset-password`

Finishing a feature `git flow feature finish 14-reset-password`

##### Using raw GIT

Starting a feature: `git checkout -b feature/14-reset-password`

Finishing a feature: 
```
git checkout develop
git merge feature/14-reset-password
git branch -d develop
```

### Commits

- Signed commits (required or recommanded ?)
- No oneliners (`git commit`, no `git commit -m`)
- 1 commit per logical change (atomical commits)

#### Format

```
<type>(<scopes>): <subject>

<description>

<footer>
```

Possible **types** (project independant)
- **build**: Building system (example : gulp, webpack, npm)
- **ci**: Continuous Integration 
- **docs**: Documentation
- **feat**: Adding a new feature
- **fix**: Bug fix
- **perf**: Performances improvment
- **refactor**: Code refacto
- **style**: Changes in code style (linting, ...)
- **test**: Tests modifications

Possible **scopes** (project dependant)
- devtools
- auth
- frontend
- backend

Formatting rules for **subject**:
- Imperative ("change", no "changed" neither "changes")
- Lowercased
- No punctuation

Formatting rules for **description**: same as for subject

Intents of the **footer**:
- Linked to Issues (that closes)
- Breaking Changes notices

### Merge request

- Merge requests should be done on Gitlab
- Merges should squash commits
- Merge requests should agregate all linked issues / breaking changes that the inside commit do.


#### Merge request validation

- n reviewer
- Test pass
- Lint pass
- Checklist

### Issue

- Explicit title
- Tagging (feat, bug, ...)
- For bug report, follow the template (TBD)
- For feature request, follow the tmeplate (TBD)

## Todo

- Clean code / clean architecture
- Namming conventions (for vars, functs, ...)