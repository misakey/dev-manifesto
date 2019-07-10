# Contributing to a Misakey project

We use Gitlab as a central tool to manage all contributions and collaborative work.

## Git

### Branches

We are using **[git flow](https://nvie.com/img/git-model@2x.png)**

So as branches we have:
- **master**: The last stable release (what is in production)
- **develop**: The newest features (waiting to be fully tested / released)
- **feat/++**: A work in progress on a feature (to merge to develop)
- **fix/++**: A work in progress to fix a bug (to merge to develop)
- **hotfix/++**: A work in progress to hotfix something in prod (to merge to master & develop)
- **release/++**: The next release preparation (to merge to master & develop)

On top of git flow:
- Branches are named lowercase, with dash between words.
- Branches names contains issue ID linked to the branch.

Basically, a branch name should look like this: `[type]/[issue-id]-[description]`

Here's the regex that validate the branch name
```
^((feat|fix|hotfix|release)\/([a-z0-9-]+)|develop|master)
```

**Process** Create the branch locally from the up-to-date version of develop. You can copy/past the
branch id / name from gitlab issues's `create merge request` button (but don't use the button to
create merge request)

### Commits

- Signed commits (required)
- 1 commit per logical change (atomical commits)

#### Format

```
<type>(<scopes>): <subject>

<optional description>
```

Possible **types** (project independant): mandatory
- **build**: Building system (example : gulp, webpack, npm)
- **ci**: Continuous Integration
- **docs**: Documentation
- **feat**: Adding a new feature
- **fix**: Bug fix
- **perf**: Performances improvment
- **refacto**: Code refacto
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

**optional description** is a free part in commit messages. 

One usage of it is to add commit names in squash commits.


Here's the regex that validate the commits
```
^(build|ci|docs|feat|fix|perf|refacto|style|test|wip)( \([a-z]+\))?: .+
```

### Merge request

MR = Merge request.

Rules:
- **Manually create the MR** (from the link when push for example)
- **Name the MR with the squash commit you want** (should follow the commits formatting)
- **Commits are squashed** (automatic)
- ~~Mention all **linked issues to close**~~ (not working on Gitlab)
- Mention all **introduced breaking changes**
- Merged after **all discussions** has been **solved** (automatic)


#### Ask a Merge Request to be reviewed

1. Review yourself the merge request (don't waste other's time)
1. Rebase on the latest version of your target branch
1. Assign people to the MR (create permanent indicator on gitlab).
1. Mention same people in a comment (create todo and temporary indicator on gitlab).
1. Don't hesitate to text people privately or on a public channel if the review is too long to you or require a quick one.

#### Review the Merge Request

- You can give feedback about the MR opening discussions on a specific line code or global to the MR.
- All discussions must be resolved in order to merge the branch.
- Discussions should never be resolved by the MR author, unless it is specified by the comment author (possibly using ⚡ (zap emoji))
- Once you have reviewed the MR, you should mention back the MR author in a comment to notify him the MR has been reviewed.

When you review a Merge Request:
1. Review the code and ensure our best practices are followed.
2. Verify the code implements functional requirements.
3. At least one person should test locally the branch. Mention you have tested the branch when you mention the MR creator about your review.

When all discussions has been resolved and you got enough approvals to merge, be sure you follow [merge the branch convention](merge-the-branch) and then you can merge !

#### Merge the branch

Squash commits. Take time to check the commit name: it should follow the commit name convention.

Ensure you have all commits inside squash commit message, Gitlab seems to not udpate it with commits added after MR opening.

Delete the source branch.

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

## Team Spirit

- Sometimes, reviews can make you feel bad, but efficiency during review is an important thing.

    "Feel free to write concise comments, get straight to the point."

    Our philosophy is to **never take personnally a feedback during a code review** even if you consider formulation is harsh or not well communicated.
    Always consider we are all here to learn from the others and to improve together.

    If you don't understand a comment and find a feedback review non constructive, feel free to ask for more details about it. If you can, do it even in face to face more better communication =) Keep in mind written communication is not the best to solve problems.

    Of course, humility and pedagogy are essential to be a good reviewer, this paragraph is mostly because of potential repetitive mistakes that lead to deshumanized review comments.

- We aim to not use gendered pronoun (prefer `their` for someone or `its` for something, or specify both `her/him`).
