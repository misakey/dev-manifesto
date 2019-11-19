# Contributing to a Misakey project

We use Gitlab as a central tool to manage all contributions and collaborative work.

## Git

### Branches

We are using the **[Trunk Based Flow](https://trunkbaseddevelopment.com)**. Its documentation is complete and easy to assimilate.
We are doing trunk freeze during release/QA process since we can't ensure new commits does not break master.

So as branches we have:
- **master**: The trunk, a stable branch.
- **feat/++**: A work in progress on a feature (based on master, to merge to master).
- **fix/++**: A work in progress to fix a bug (based on master, to merge to master).
- **hotfix/++**: A work in progress to hotfix something in prod (based on production tag, to tag then to merge to or cherry-pick on master).

- Branches are named lowercase, with dash between words.
- Branches names contains issue ID linked to the branch.

Basically, a branch name should look like this: `[type]/[issue-id]-[description]`

Here's the regex that validate the branch name
```
^((feat|fix|hotfix)\/([a-z0-9-]+)|master)
```

**Process** Create the branch using the button `create merge request` from gitlab's issues.

### Commits

- Signed commits (required).

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
^(build|ci|docs|feat|fix|perf|refacto|style|test|wip)(\([a-z-]+\))?: .+

```

### Merge request

MR = Merge request.

Rules:
- **Create the MR from Gitlab Issues while creating the branch**.
- **Name the MR with the squash commit you want** (should follow the commits formatting).
- **Commits are squashed** in order to show iterative integration of features (still you may merge many commits).
- Mention all **introduced breaking changes**.
- Merged after **all discussions** has been **solved** (automatic).
- At least two reviewers & one tester (can be a reviewer).

#### Ask a Merge Request to be reviewed

1. Rebase on the latest version of master branch ([here are some hints about how to rebase your branch](#rebase-your-branches)).
1. Review yourself the merge request (don't waste other's time).
1. Assign people to the MR (create permanent indicator on gitlab & add a "to do" notification).
1. Don't hesitate to text people privately or on a public channel if the review is too long to you or require a quick one.

#### Review the Merge Request

- You can give feedback about the MR opening discussions on a specific line code or global to the MR.
- All discussions must be resolved in order to merge the branch.
- Discussions should never be resolved by the MR author, unless it is specified by the comment author (possibly using ⚡ (zap emoji)).
- Once you have reviewed the MR, you should assign back the MR author in a comment to notify them the MR has been reviewed.
- If the MR has two approvals (including your future one) and it is not tested, you should test it.

When you review a Merge Request:
1. Review the code and ensure our best practices are followed.
2. Verify the code implements functional requirements.
3. Mention if you have or not tested the branch.

When all discussions has been resolved and you got enough approvals to merge, be sure you follow [merge the branch convention](merge-the-branch) and then you can merge !

#### Merge the branch

Squash commits. Take time to check the commit name: it should follow the commit name convention.

Ensure you have all commits inside squash commit message, Gitlab seems to not udpate it with commits added after MR opening.

Delete the source branch.

## Team Spirit

- Sometimes, reviews can make you feel bad, but efficiency during review is an important thing.

    "Feel free to write concise comments, get straight to the point."

    Our philosophy is to **never take personnally a feedback during a code review** even if you consider formulation is harsh or not well communicated.
    Always consider we are all here to learn from the others and to improve together.

    If you don't understand a comment and find a feedback review non constructive, feel free to ask for more details about it. If you can, do it even in face to face more better communication =) Keep in mind written communication is not the best to solve problems.

    Of course, humility and pedagogy are essential to be a good reviewer, this paragraph is mostly because of potential repetitive mistakes that lead to deshumanized review comments.

- We aim to not use gendered pronoun (prefer `their` for someone or `its` for something, or specify both `her/him`).


## Frequently asked questions


### Rebase your branches

Following our flow, you will have at some point to rebase your branch on `master`.

Rebase can be done in many ways, what is important to know is the states of your respective branches.
- do not hesitate to rebase your branches against `master` after a big MR has been merged (on which you should be aware as a reviewer / project contributor).
- branches created in cascade can be problematic for rebase strategy, so you should try to limitate it as much as possible or you'll have to cascade rebase all your branches.
- when needed, `git push --force-with-lease` (safer than --force).
- see `git rerere` when you have lot of redundant conflict to solve while rebasing many commits (or see next section).
- some people might appreciate some existing merge tool to facilitate conflict resolutions (`beyond compare`, `kdiff3`...).
- reminder that if someone has your work locally, rewriting history might create painful situations.

#### Squash first using interactive rebase on your own branch

The most common issue with rebase strategy is that conflicts are resolved one commit by one commit rebasing your branch.
You can easily avoid that by first squashing your commits before rebasing your branch.

You can do it by using `git rebase -i` on your own branch:

1. Find the last commit from master on your branch (the most recent commit after you just created your branch).
2. `git rebase -i {commit_hash}`.
3. Choose to squash your commits.
4. Rebase finally against `master`: you just have one conflict to solve.

Considering your commit are squashed, you can do it whatever you want on your branch in term of source management, you can have merge commits if you need it from other branches, or if you need to work simultaneous on a branch with another contributor.

#### Think about cherry-pick

Sometimes, you can have a lot of commits that have been added to `master` branch while you were developing (or in case of a hotfix).

Instead of rebasing this commit and resolving potential conflict with `X` new commits, you can, after being sure your commit is saved remotely, choose to `reset --hard` your branch on `master` then `git cherry-pick {commit_hash}`.
This way, you will resolve all conflict in one row and it will save you time.
