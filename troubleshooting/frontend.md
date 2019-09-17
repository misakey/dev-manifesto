# Frontend Troubleshooting

## ESLint may stop working because of cache issues

Just an issue to document a weird bug I (@cedricvanrompay) had and how I solved it with @WaSa42.

ESLint was reporting many errors, only of type import/no-unresolved, for one specific package,
when the CI pipeline (and everyone else's linting) was passing.

Turns out that the command run by the CI pipeline (yarn lint:ci)
is not exactly the same as the one we use (yarn lint),
and the difference is that we use the --cache option while the CI doesn't.

When I used yarn lint:ci (that is, eslint . --report-unused-disable-directives --ext .js,.md),
linting passed, showing that the problem came from my cache indeed.

What's more, after this even yarn lint (or yarn test which calls it) where working again,
so I guess using the command without cache somehow cleaned the cache.
