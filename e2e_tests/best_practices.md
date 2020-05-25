# Team best practices

This document contains our recommendations regarding best practices when writing tests with Cypress.

You will find Cypress team's best practices [here](https://docs.cypress.io/guides/references/best-practices.html) 

## UI and user driven tests

Make tests closest as possible to how user visits the application.

Focus on what the user sees. Also include screen readers in that concept.

With a bit of knowledge on ARIA and what user sees, decide together how to interact with application through cypress.

To discuss through mumble.

## Define application state through UI/UX to have easy tests

In tests, after triggering some interactions within the application, we may want to assert a so-called application state.

Applying user driven perspective, this application state must be verified via UI state.

Therefore, in each of these tests, we will need to define a satisfying way to check UI state. 

This does not mean seeking every bit of UI changed by a specific app state transition, but the core ones.

### Examples

#### Application state = being connected

- How does a user know (through UI) when he is connected ?

When user is connected, button connect transforms into an avatar.

> There are other changes, but this one is by far the most significant to validate this application state.

#### Application state = being disconnected

- How does a user know (through UI) when he is disconnected ?

When user is disconnected, most screens display button connect.

:warning: Some don't, so we might need other ways to check this application state for those screens.

#### Application state = successful connection

- How does a user know (through UI) when he just connected successfully ?

When auth flow worked, user is redirected, button connect transforms into avatar, a snackbar with a success text is displayed, etc.

To define this application state, discuss what is mandatory to check and what is overkill.

Here, snackbars are an overkill check, because their behaviour is by definition not core to an application behaviour.

**But**, we could definitely work on snackbar behaviour and consistency through the whole app by creating e2e tests focusing only on when they should appear in application.

### Look for obvious UI changes

Most obvious things we could check:
- existing / not existing elements
- visible / not visible elements
- disabled elements
- errors (red colored text)
...

See [interacting with elements](https://docs.cypress.io/guides/core-concepts/interacting-with-elements.html) for an exhaustive list of cypress abilities.

## Selecting elements in dom

[Read section 1](https://medium.com/javascript-in-plain-english/how-to-get-the-best-of-ui-test-automation-using-cypress-and-ci-continuous-integration-f9c5f056b364)

### Risk of broken selectors with UI changes

Basing selectors on not obvious / long term criterias might create unexpected broken tests whenever we change the app.

I personnally like using "user driven" selectors, because tests become less technical and more related to the UI.
Best when possible and not risky would be to base selectors on stuff visible to user.

#### Pitfalls
- **base all selectors only on text**: makes them dependent to I18n and changes to text. There can also be false positives because some texts are repeated across page.
- **base selectors on css classes**: currently impossible because of our jss library, classes are not reliable.
- **base selectors on xpath (dom hierarchy)**: makes them highly dependent on design, which isn't reliable as we may change dom for unrelated purposes.
- **add specific attributes to DOM for tests + base selectors on them**: makes development heavier and relationship between dev and e2e tests is not strong enough yet. **recommended by cypress**

#### My recommendation

- **make use of DOM meaningful attributes, add them to elements when they are missing**

That's the target, for future dev, but it's not mandatory to refacto the whole app to do tests in a first time.

Meaningful DOM elements, such as inputs, buttons and specific Misakey elements should be recognizable through DOM.

If they aren't, maybe it's something which should change in a refactor.

Misakey components' selectors could be defined once in a specific file, to make them easy to evolve with code.

A submit button is fairly easy to find: `button[type=submit]`, but it lacks one extra criteria to make it unique, it could be an id, an attribute or inner text.

- **make use of a11y oriented attributes (`name`, `label`, `aria-`) whenever they exist**
- **factorize selectors in a file when they are used multiple times**

This way, it'll be easy to fix them whenever they are broken.

## Code splitting

### Maximize DOM-related factorization in tests

Example
![image](resources/e2e_tests/dom-factorization.png)

This code factorization is very easy. In our context it is important to have maximal flexibility in tests regarding application changes.

Application logic very rarely changes, but structure does.

Having maximal factorization regarding app structure makes changes in tests very simple.

For example:
- "input for identifier", we may change attributes, not logic "type identifier in input".
- "button connect", same
...

Always write tests with that in mind.

### Create [custom commands](https://docs.cypress.io/api/cypress-api/custom-commands.html) for important reusable features

:warning: Implement commands only to enforce best practices. [Don't make everything a custom command](https://docs.cypress.io/api/cypress-api/custom-commands.html#1-Don%E2%80%99t-make-everything-a-custom-command).

### Use [aliases](https://docs.cypress.io/guides/core-concepts/variables-and-aliases.html) and [custom commands](https://docs.cypress.io/api/cypress-api/custom-commands.html) to factorize selectors

[aliasing DOM elements](https://docs.cypress.io/api/commands/as.html#Syntax) allows to factorize how we select an element in a test suite.

creating custom commands for generic rules about selectors allows to factorize how we expect to select specific elements in a reusable and factorized way.

Therefore if a selector is broken because of a change in application, fixing this will take only one sec:
- check / update command
- check / update aliased selector

## Handling server data

For now server data will be handled out of cypress with populators and `test-and-run` features.

In a first step we might need to `make reset-db` before starting some e2e tests.

We could also write test suites creating new data on every run.

We will see when we face issues, such as errors when testing account creation.

## To challenge: using cypress for some unit tests

In [this video](https://www.youtube.com/watch?v=5FnalKRjpZk), Gleb Bahmutov explains that unit tests and integration tests are the same thing from a technical perspective.

Cypress could allow us to write UX oriented "unit tests".

From a functional test perspective, we can test isolated components.

There is a [dedicated recipe chapter](https://docs.cypress.io/examples/examples/recipes.html#Unit-Testing) for that.

I think the tool could give us extra possibilities regarding unit tests and become a good addition to storybook.

I see a use case for our very stable and reused "ui lib components".

# Good reads

- [medium article](https://medium.com/javascript-in-plain-english/how-to-get-the-best-of-ui-test-automation-using-cypress-and-ci-continuous-integration-f9c5f056b364)