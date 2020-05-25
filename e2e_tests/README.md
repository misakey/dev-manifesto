# Writing end-to-end tests

We use [Cypress](https://www.cypress.io/) to write e2e tests.

The following documentation aims at giving you the knowledge to work with the tool.

To get basic understanding on Cypress and how it works to update a test, I recommend you to read quick start.

To have a satisfying MR with new tests, please also read best practices.

## Table of Contents

- [Quick Start](#quick-start)
- [Best Practices](#best-practices)
- [Going Further](#goig-further)
  - [GUI](#gui)
  - [API](#api)
  - [Assertions](#assertions)
  - [Recipes](#recipes)
  - [IDE integration](#ide-integration)
- [Issues Questions](#issues-questions)

## Quick start

### [Overview presentation](https://vimeo.com/237527670)

### [Core concepts](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress.html#Cypress-Can-Be-Simple-Sometimes)

### How to run cypress on project

Run in `test-and-run`

- `make cypress` to run tests in CLI
- `WORKING_ON="cypress" make cypress` to run tests in GUI

### Write my first test

In project `test-and-run`

#### Check existing test files

You can find tests in `cypress/cypress/integration/*`

Have a look at existing tests for a first grasp of what's possible with cypress.

#### Check custom commands

Custom commands are extra methods we can add to cypress context to extend its features with access to `cy` context.

Custom commands are located in `cypress/cypress/support/commands.js`.

#### Small introduction

Check [How to run cypress on project](#how-to-run-cypress-on-project).

Run cypress.

In project `test-and-run`, go to file `signIn.spec.js` (full path: `cypress/cypress/integration/signIn.spec.js`)

In first test (`SignIn => should successfully login`), replace typed identifier (l.21) by `pp@vp.com`

Test runner should rerun.

Check identifier changed.

## Best practices

### [Cypress best practices](https://docs.cypress.io/guides/references/best-practices.html)

Also watch these talks:
- [Brian Mann - Cypress]((https://www.youtube.com/watch?v=5XQOK0v_YRE)
- [Gleb Bahmutov - Cypress](https://www.youtube.com/watch?v=5FnalKRjpZk&t=27s)

### [Our own](e2e_tests/best_practices.md)

## Going further

### [GUI](https://docs.cypress.io/guides/core-concepts/test-runner.html)

### [API](https://docs.cypress.io/api/api/table-of-contents.html)

#### [Type text inside inputs](https://docs.cypress.io/api/commands/type.html#Syntax)

NB: special keyboard keys.

### [Assertions](https://docs.cypress.io/guides/references/assertions.html)

:warning: There are a lot of aliases coming from chai and sinon.

Also be careful not to mix them with jest assertions.

#### [Most commands perform assertions by default](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress.html#Default-Assertions)

### [Recipes](https://docs.cypress.io/examples/examples/recipes.html)

### [IDE integration](https://docs.cypress.io/guides/tooling/IDE-integration.html)

- seems useful for vscode: [cypress helper](https://marketplace.visualstudio.com/items?itemName=Shelex.vscode-cy-helper)

## Issues Questions

### Using cypress with docker limits IDE integration and code completion

Code completion help coming from vscode and [documented here by cypress](https://docs.cypress.io/guides/tooling/IDE-integration.html#Visual-Studio-Code) requires cypress package to be installed locally.

### Implement a programmatical way to log in for e2e tests

[Recommended by Cypress](https://docs.cypress.io/guides/getting-started/testing-your-app.html#Fully-test-the-login-flow-%E2%80%93-but-only-once).

Reasons:
- shorter delay for tests requiring to be logged in if we don't repeat login test
- login test already covers logging in

**I don't really like this logic** but I have to admit it takes about 10sec to log in through UX, hence it might be worth to have quicker e2e tests.

**Is there a simple way to implement that ?**

Script we might use in `test-and-run` `tools/get_access_token.py`

Cypress gives some recipes [here](https://docs.cypress.io/examples/examples/recipes.html#Logging-In)