# Front-end Questions & Answers
Here you can find **short** answer on various topics of the front-end development.

## Contribute
* You can Ask a question by creating an issue following
[the same guidelines as StackOverflow's ones](https://stackoverflow.com/help/how-to-ask).
* Then you can create a Merge Request with your question and the issue linked like this:

```markdown
### How do I ask a good question ?
A discussion is opened here: https://stackoverflow.com/help/how-to-ask
```
* When the topic is closed, the person that asked the question make a short answer
or create a new section in the frontend folder if needed.

## Questions

* [What is the main stack ?](#what-is-the-main-stack-)
* [Is there a default UI library ?](#is-there-a-default-ui-library-)
* [Do we strongly type ?](#do-we-strongly-type-)
* [Are there test processes ?](#are-there-test-processes-)
* [Do we have external packages ?](#do-we-have-external-packages-)
* [Do we translate texts ?](#do-we-translate-texts-)
* [Do we follow a state pattern ?](#do-we-follow-a-state-pattern-)
* [Do we have data validation ?](#do-we-have-data-validation-)
* [Are we importing with absolute or relative path ?](#are-we-importing-with-absolute-or-relative-path-)
* [Can we use docker ?](#can-we-use-docker-)
* [Are there CI pipelines ?](#are-there-ci-pipelines-)
* [Are we considering Server Side Rendering ?](#are-we-considering-server-side-rendering-)
* [How do we handle heads and metas ?](#how-do-we-handle-heads-and-metas-)
* [How do we catch errors in components ?](#how-do-we-catch-errors-in-components-)

### What is the main stack ?
We bootstrap project with Create React App that implements React an Webpack.
We add Redux pattern on top.

### Is there a default UI library ?
Yes. Our theming / UI is based on [material-ui](https://material-ui.com/).
We also use our custom UI package which is @misakey/ui.

### Do we strongly type ?
We don't use external typing libraries like Typescript,
but we are highly rigorous with the PropTypes.

### Are there test processes ?
A discussion is opened here: https://gitlab.com/Misakey/pages-roses-frontend/issues/57

### Do we have external packages ?
Yes currently we have have:
- **@misakey/API** - Instance of class API that can easily bind request in JS
- **@misakey/helpers** - Our own set of helpers extending Lodash ones
- **@misakey/hooks** - Our own set of hooks (useWith, useTimeout...)
- **@misakey/ui** - Reusable React components

### Do we translate texts ?
Yes. All our apps are internationalized from day 1.
For doing that we use the [react-i18next](https://react.i18next.com) package.

### Do we follow a state pattern ?
Yes. For store management we use [redux](https://redux.js.org/).

### Do we have data validation ?
Yes. For data validation (including form validation) we use [yup](https://github.com/jquense/yup).

### Are we importing with absolute or relative path ?
Absolute path (in most case).
See more details in [Import section](react.md#import).

### Can we use docker ?
Yes. Most projects are working with Docker.
We have two different Dockerfiles:
- **Development** use the `yarn start` script, to have the full development server (hot reloading, ...)
- **Production** need to build the app bundle, then to serve it in a much lighter image

### Are there CI pipelines ?
Yes. We use gitlab-ci as a CI. Today, we just have linting running in the CI. 

### Are we considering Server Side Rendering ?
We didn't break that subject totally for now. Here a state of our searches:

* We don't want to use SSR everywhere. Just in the SEO-critic pages for now
* react-dom + express seems to be a good first move
* For performance reason, we probably want to put it behind a CDN ? (not sure)
* We need to check if we can pre-generate pages that we need (the main SSR subject is to make it work with Les Pages Roses)

### How do we handle heads and metas ?
We thought to use [react-helmet](https://github.com/nfl/react-helmet) to manage the `<head>` section, but the project seems depreciated (see [this issue](https://github.com/nfl/react-helmet/issues/451))
So in the `@misakey/ui` package we (will) define a component to manage dynamically `<title>` and `<meta>` tags.

### How do we catch errors in components ?
We use [error boundaries](https://reactjs.org/docs/error-boundaries.html) for managing errors in our app: 
- overall error boundary in the route of the project, that shouldn't be triggered, but will run a fallback UI if something break in a high level of the app
- component error boundary from components that have a chance to break, and that shouldn't break all the app (like widgets)
