# React
Guidelines and thought about react development.

## Table of Contents
* [Eslint](#eslint)
* [Hooks](#hooks)
* [Import](#import)
* [Redux](#redux)

## Eslint
We use [eslint](https://eslint.org/) for code linting.
The rules we're using are based on Airbnb's ones.
We tweak some rules on top of that.

```json
{
  "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],
  "react/forbid-prop-types": [1, { "forbid": ["any", "array"] }],
  "import/prefer-default-export": 0,
  "object-curly-newline": "off"
}
```


## Testing

### Unit Tests

We use [Jest][] for testing.
You don't have to install it separately,
it is installed by [CRA][] in every new project.
As a result every React project should have Yarn scripts available to launch tests;
you can find them in the file `package.json`
at the root of a project,
in Section `scripts`.
For instance in [project JS Common](https://gitlab.com/Misakey/js-common)
you can run `yarn test:unit crypto`
to run all test files containing the string `crypto` in their path.
(or just `yarn test crypto` to launch both linting and testing).

See Jest documentation to see how to write tests:
https://jestjs.io/docs/en/getting-started

In terms of file structure,
a test file must have its name ending with `.test.js`,
must be located next to the file it is testing,
and must have the same scope.
For example,
if you are testing a helper exporting 2 named functions,
file structure and content layout should be:

```
$ ls twoNamed/
index.js  index.test.js
$ cat twoNamed/index.test.js
import {namedOne, namedTwo} from './index';

describe('testing helper twoNamed', () => {
  describe('testing namedOne', () => {});

  describe('testing namedTwo', () => {});

});
```


### Unit Tests with (mocked) HTTP Calls

HTTP calls must be [mocked](https://jestjs.io/docs/en/mock-functions) in unit tests.
Here is an example  showing how to mock HTTP calls
that are supposed to return JSON data
(see documentation of
[`jest.spyOn`](https://jestjs.io/docs/en/jest-object#jestspyonobject-methodname)
and [mock functions](https://jestjs.io/docs/en/mock-function-api)
for more info):

```javascript
// test suite setup/teardown
// see https://jestjs.io/docs/en/setup-teardown

beforeAll(() => {
  jest.spyOn(global, 'fetch');
});

beforeEach(() => {
  fetch.mockReset();
});

afterAll(() => {
  fetch.mockRestore();
});

// end of setup/teardown

test('makes valid HTTP calls', async () => {
  const mockedResult = { whatever: ['JSON', 'object'], you: 'want' };

  fetch.mockResolvedValue(new Response(
    new Blob([JSON.stringify(mockedResult, null, 2)], { type: 'application/json' }),
  ));

  // do not forget "await",
  // otherwise the call to fetch will never happen
  const result = await functionWhichIsSupposedToCallFetch(args);

  // checking (mocked) fetch was indeed called
  expect(global.fetch).toHaveBeenCalledTimes(1);

  // you can read the arguments with which fetch was called
  expect(decodeURIComponent(global.fetch.mock.calls[0][0].url)).toEqual(expectedUrl);

  expect(result).toEqual(whateverYouExpected);
});

```


### Integration Tests with real HTTP Calls

You may want to run tests
where your JS code actually makes HTTP calls
to some server
(be it the real one or a test server),
that is, integration tests.
First, note that **these tests must not be part of the unit tests**
(they are too heavy for this)
and must not be part of the CI jobs.
Instead, we use a suffix that won't be recognized by Jest test discovery mechanism: `.int-test.js`.
We create a file `jest.integration.config.js` to override Jest's Regex
for when we want to run these integration tests (locally):

```javascript
const jestConfig = require('./jest.config');

jestConfig.testRegex = '\\.(int-test)\\.js$';

module.exports = jestConfig;
```

Add a script in `package.json`
which will use this modified configuration:
```json
"test:integration": "cross-env NODE_ENV=test jest -c jest.integration.config.js",
```

Finally, NodeJS (the platform used by Jest)
does not have `fetch` by default
so you need to provide it yourself
by doing `yarn add --dev whatwg-fetch`
then creating a small JS file containing just `import 'whatwg-fetch'`,
and register it as a setup file for Jest by adding the following to your `jest.config.js` file:

```javascript
module.export = {
  ...
  setupFiles: [
    './path/to/your/file.js',
  ],
}
```


## Hooks


## Import


## Redux




[Jest]: https://jestjs.io
[CRA]: https://create-react-app.dev/
