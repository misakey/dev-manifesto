# Contributing to a Misakey project

We use Gitlab as a central tool to manage all contributions and collaborative work.

## Git

### Branches

We are using **[git flow](https://nvie.com/img/git-model@2x.png)**, we advise you to use the [git flow CLI](https://danielkummer.github.io/git-flow-cheatsheet/)

So as branches we have:
- **master**: The last stable release (what is in production)
- **develop**: The newest features (waiting to be fully tested / released)
- **feature/++**: A work in progress on a feature (to merge to develop)
- **bugfix/++**: A work in progress to fix a bug (to merge to develop)
- **hotfix/++**: A work in progress to hotfix something in prod (to merge to master & develop)
- **release/++**: The next release preparation (to merge to master & develop)

On top of git flow:
- We add the issue ID linked to the feature (or the hotfix if existing), before the name of the feature (or the hotfix).
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

- Signed commits (required)
- 1 commit per logical change (atomical commits)

#### Format

```
<type>(<scopes>): <subject>

<description>

<footer>
```

Possible **types** (project independant): mandatory
- **build**: Building system (example : gulp, webpack, npm)
- **ci**: Continuous Integration 
- **docs**: Documentation
- **feat**: Adding a new feature
- **fix**: Bug fix
- **perf**: Performances improvment
- **refactor**: Code refacto
- **style**: Changes in code style (linting, ...)
- **test**: Tests modifications

Possible **scopes** (project dependant): optional
- devtools
- auth
- frontend
- backend
- ...

Formatting rules for **subject**: mandatory
- Imperative ("change", no "changed" neither "changes")
- Lowercased
- No punctuation

Formatting rules for **description**: optional

Intents of the **footer**: optional
- Linked to issues (to close it automatically)
- Breaking Changes notices (if unavoidable breaking changes)

### Merge request

- Merge requests should be done on Gitlab
- Merges should squash commits
- Merge requests should aggregate all linked issues solved and breaking changes introduced by the commits.

#### Merge request validation

- n reviewer
- Test pass
- Lint pass
- Checklist

## Project managment

We use the Gitlab issues to manage the projects.
We use the board view to have a kanban view.


### Boards / Kanban

Here's the [list of labels](https://gitlab.com/Misakey/contributing/labels) we are using as step in the issue workflow.

We use the global Misakey wide board to have an overview of the progress of the work/sprints.
In order to make it work, we need to follow some conventions in the labelling of the issues:
- all backend issues are labelled with the `Backend` label
- for each project we use the `project-name` label corresponding to the issue. This helps us to easily switch between project in this overview

### Issue naming

- Explicit title
- Tagging (feat, bug, ...)
- For bug report, follow the template (TBD)
- For feature request, follow the template (TBD)
- Features issues should begin with As a user, I [...]