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

## Hooks

## Import

## Redux
