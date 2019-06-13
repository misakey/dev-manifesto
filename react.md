# React guidelines

Describes the guidelines for React frontend development.
This documentation contains guidelines and thought (for evolution of the usages for example)  

## Table of Contents

* [Base project](#base-project)
    * [CRA, Webpack & config](#cra-webpack--config)
* [Dependencies](#dependencies)
* [Folder Architecture](#folder-architecture)
* [Docker & envs](#docker--envs)
* [CI & tests](#ci--tests)
* [Misc](#misc)
    * [Error Management](#error-management)
    * [Style](#style)
    * [Head management](#head-management)
    * [Server Side Rendering](#server-side-rendering)
    * [Node package vs Git Sub-modules](#node-package-vs-git-sub-modules)
* [Improving the guidelines](#improving-the-guidelines)

# Base project

A complete project base is available in the [React Template](https://gitlab.com/Misakey/templates/react).
This template is a technical implementation of everything described in the present document.
-> A question is open about the interest of such a project (as the practices may evolve fast, it may be depreciated quickly)

## CRA, Webpack & config

For now we're using CRA as a base of our projects.
We don't want to eject: it would be too much work to maintain the scripts with further updates.

So if we need to do some easy webpack tweaks, we would use a module like [react-app-rewired](https://github.com/timarney/react-app-rewired).
-> It's an easy-to-maintain way to be able to have access to some webpack configuration.

If we need a full control over the configuration, we would fork the create-react-app, and modify on it the react-scripts package to suit our needs.

# Dependencies

## Eslint

We use [eslint](https://eslint.org/) for code linting.
The rules we're using are based on Airbnb's ones. We tweak some rules in top of that (more details in the [React Template](https://gitlab.com/Misakey/templates/react))

## Formik

For form management we use [formik](https://jaredpalmer.com/formik/) (and [Yup](yup) for form validation).
So all forms should be wrapped with Formik

## Material UI

Our theming / UI is based on [material-ui](https://material-ui.com/). We use their components for grid system, UI kit, Icons, ... 
We're using their theming utility only for typeface and default color on components.

## Misakey UI

All components that could be reused in another project (form fields, avatar, ...) should be extracted in our component library: [misakey-ui](https://gitlab.com/Misakey/react-components).

This component library provide components, but also some business rules (for input validation for example).

## Proptypes

We use [prop-types](https://github.com/facebook/prop-types) to set the types of props & default props on all components.

## React I18Next

All our apps are internationalized from day 1 (mini: French & English).
For doing that we use the [react-i18next](https://react.i18next.com) package.

## React Router

For routes management, we use [react-router-dom](https://reacttraining.com/react-router/web/) package.

We use an over-layer of the `Route` component. This overlayer enable for now two features:
- check that the path is well defined (and throw an error if not)
- enable private routes that require to be logged-in.

## Redux

For store management we use [redux](https://redux.js.org/).

We use the practice to decompose the store management with action creators (and not building actions on the fly).

To be able to identify easily the action creator, we post-fix the functions name with `Action`.

## Yup

For data validation (including form validation) we use [yup](https://github.com/jquense/yup).

# Folder Architecture

## Overview

The decomposition of the app is done this way:
- the root component in is `src/App.js` (mounted from the main `src/index.js` file). This component compose all the global providers:
    * A global ErrorBoundary
    * The I18N provider
    * The store Provider
    * The theme provider
    * Then instantiate the router
- The router define all the routes of the app, and set the corresponding screen. The routes are defined in another file (to be available for other uses like redirecting or definition of links)
- the visual base of the app is a screen
  - a screen component hold the logic
- a screen use a layout
  - a layout contains only the structure of the page (header / footer for example)
- as child or props of the layout, the screen set the components used for the screen
  - if the component is specific to this screen, it should be defined as a sub-folder of the screen folder
  - if the component is reused (or will be reused) by another screen, it should be defined in the `src/components` folder
    - the same logic is applied for sub-components of components: if it's reused by another component: `src/components` else create the folder 

- all the interactions with the API are defined in the `/src/api` folder
  - the API management is done with an API client, that is *for now* copied in every projects, and will be extracted to a specific package
  - the API calls are defined in files in the `api` folder and are organized by category of calls. Those categories are business logic dependent. 
- the store is defined in the `src/store` folder
  - the `src/store/index.js` file initialize the store (apply middleware, import reducers, ...)
  - the `src/store/reducers` define all reducers in one file and an overall export in the `index.js` file
  - the `src/store/actions` define actions by reducer in separated files and an overall export in the `index.js` file
  - the `src/store/selectors` define store selectors (for selecting subset of the store, or combining information)
- the locales files are defined in the `public` folder, to be available over XHR ([XML HTTP Request](https://developer.mozilla.org/en/docs/Web/API/XMLHttpRequest))

## Addendum

In the `jsconfig.js` we define `baseUrl: 'src'` as a compiler option to make absolute path possible. 

This way from anywhere in the app you can use absolute path from inside the src folder. 
For example: `import * from 'components/ReusableComponent1`

## File-system tree

```
├── public
│   ├── img
│   │   └── allIOsAndAndroidIcon.png # used in the index.html file
│   ├── locales
│   │   ├── en
│   │   └── fr
│   │       ├── namespace1.json
│   │       └── namespace2.json
│   ├── env.js # Mandatory file for env managment (not using ENV vars anymore)
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
├── src
│   ├── api
│   │   ├── APIClient
│   │   │   └── index.js
│   │   ├── apiCallCategory2js
│   │   ├── apiCallCategory1.js
│   │   └── index.js
│   ├── components
│   │   ├── ReusableComponent1
│   │   │   ├── SpecificSubComponent
│   │   │   │   ├── index.js
│   │   │   │   └── SpecificSubComponent.js
│   │   │   ├── index.js # Just exporting the ReusableComponent1 from ReusableComponent1.js
│   │   │   ├── ReusableComponent1.js
│   │   │   └── ReusableComponent1.scss
│   │   ├── ReusableComponent2
│   │   └── ReusableComponent3
│   ├── layouts
│   │   └── Layout1
│   │       ├── LayoutSubpart1
│   │       │   ├── index.js
│   │       │   └── LayoutSubpart1.js
│   │       ├── LayoutSubpart2
│   │       ├── index.js
│   │       └── Layout1.js
│   ├── router
│   │   ├── index.js # Just exporting Router & ROUTES
│   │   ├── Router.js
│   │   └── routes.js
│   ├── screens
│   │   ├── Screen1
│   │   │   ├── index.js
│   │   │   └── Screen1.js
│   │   ├── Screen2
│   │   └── Screen3
│   ├── store
│   │   ├── actions
│   │   │   ├── index.js # Exporting actions and types
│   │   │   ├── substore1Actions.js  
│   │   │   ├── substore2Actions.js
│   │   │   └── types.js
│   │   ├── reducers
│   │   │   ├── index.js # Exporting the combined reducer
│   │   │   ├── substore1Reducer.js
│   │   │   └── substore2Reducer.js
│   │   ├── selectors
│   │   │   ├── index.js
│   │   │   ├── substore1Selectors.js
│   │   │   └── substore2Selectors.js
│   │   ├── store.js
│   │   └── index.js
│   ├── styles
│   │   ├── style.scss
│   │   └── theme-mui.js
│   ├── utils
│   │   └── i18n
│   │       ├── i18n.js
│   │       └── index.js # exporting the i18n object
│   ├── App.js
│   └── index.js
├── Dockerfile # Build dockerfile
├── Dockerfile.dev # Dev dockerfile
├── jsconfig.json
├── package.json
├── README.md
└── yarn.lock
``` 

# Docker & envs

## Docker

We have two different Dockerfiles for the projects

- **Development** we use the `yarn start` script, to have the full development server (hot reloading, ...)
- **Production** we need to build the app bundle, then to serve it in a much lighter image

## Env management

We want to be able to build Docker images that can be used either in a dev or prod environment. 
Doing that will require an env management that is independent from the compiler.

To do that we put all environment variables in an file (`public/env.js`) that is called in the `public/index.html` before the react bundle.
This file just contain the environment definition, and put it in `window.env`

So if you need an environment variable in the code, it will be available in the `window.env` object.

To make it work, you need to: 
- **for dev env**: mount the dev conf file as a volume in the docker-compose 
- **for prod env**: copy the prod conf file in the container

# CI & tests

We use gitlab-ci as a CI. 
Today, we just have linting running in the CI. 

## Tests

For now no tests are used in the projects. We project to implement some when the more experienced developers will come:
- Snapshots (freeze a component state, and check if new version of code match the frozen state or not)
- Unit test for algorithm parts of the code

# Misc

## Error management

### Error boundaries

We use [error boundaries](https://reactjs.org/docs/error-boundaries.html) for managing errors in our app: 
- overall error boundary in the route of the project, that shouldn't be triggered, but will run a fallback UI if something break in a high level of the app
- component error boundary fro components that have a chance to break, and that shouldn't break all the app (like widgets)

### API Errors

API Errors are managed by the API client. It'll return an error object that will be consistent if the error is a network error, an API return error, ...

## Style

The style of the app is managed with SASS. We don't use CSS in JS.

We have an overall SCSS file in the `src/style` folder, that define overall variables (typos, colors). This file will be extracted in the `misakey-ui` project

All components (layouts, components) have a SCSS file defined in the component folder to define component specific 

### Material UI

We define Material UI theme in the Material UI configuration object. In this object we define:
- the colors
- the typos

## Head management

We thought to use [react-helmet](https://github.com/nfl/react-helmet) to manage the `<head>` section, but the project seems depreciated (see [this issue](https://github.com/nfl/react-helmet/issues/451))

So in the `misakey-ui` package we (will) define a component to manage dynamically `<title>` and `<meta>` tags.

## Server Side Rendering

We didn't break that subject totally for now. Here a state of our searches:
- We don't want to use SSR everywhere. Just in the SEO-critic pages for now
- `react-dom` + express seems to be a good first move
- for performance reason, we probably want to put it behind a CDN ? (not sure)
- We need to check if we can pre-generate pages that we need (the main SSR subject is to make it work with Les Pages Roses)

## Node package vs Git Sub-modules

A question is present about using git sub-modules or npm packages for our common external resources (API Client, UI Kit, ...). 

Today the `misakey-ui` is a package on NPM, and it's really slowing down the processes. A part of that is caused by the lack of experience in doing external packages, and we could gain a lot of the experience on that subject.

The API Client isn't created yet. It should be used as a git submodule, because it really seems to be a versioned logic (and maybe when will be stable / when we'll have enough automation, we would be able to put it on NPM)

# Improving the guidelines

If you want to improve the guidelines, here's the process to follow:
1. Check with the team that your improvement is a good idea / not already thought (informal discussion)
2. Create a merge request on the present guidelines. Make it approved by all the frontend team (everyone should be aware of the evolution of this document)
3. Implement the modifications in the [React Template project](https://gitlab.com/Misakey/templates/react) to be sure your improvements are applicable and well designed. Make a MR about it
4. If some modifications should be done (revealed by the 3rd step) go back to step 2
5. Once it's all good, you can implement it into all frontend projects

As you can see, modifying the guidelines is a heavy process. It shouldn't block you to improve it, but in a mid term, the guidelines should be stable (that's why it's important to take time to think about the big picture in the review step)