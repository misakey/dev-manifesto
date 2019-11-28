# Hooks Cheatsheet

Here you can find **short** tricks on various hooks use cases.

## UseRef

This hook is not very often used in our codebase.

It is very powerful though as it is the only hook allowing you to store data without triggering any re-render on update.

It has 2 main uses:

1. as a dom ref, it allows you to call public functions on dom nodes, such as `.focus()` for instance.
2. as a reference holding a value

### Dom ref

pretty straightforward.

### Reference holding a value

`useRef` allows you to store a value and update it independently of the rest of the lifecycle of your component.

It can be useful combined with `useEffect` when you don't want to trigger your effect when the ref value changes.

The main downside of this use is that as it does not trigger a re-render of your component, you can't rely on a `useRef` value to handle rendering.

#### TL;DR

* `useRef` cannot work for render conditions in a component
* `useRef` can be useful combined with `useEffect` to avoid triggering when ref changes

#### Examples

* `js-common` => `packages/hooks/src/useTimeout/index.js`

## UseEffect

This hook is the go to for mount / update / unmount lifecycle.

### Which dependencies to pass or not?

Read this [doc + the footnote](https://reactjs.org/docs/hooks-reference.html#conditionally-firing-an-effect)

Be careful about stale referenced values as it is very tough to debug.

### Call only on mount/unmount

The function passed in `useEffect` will always atleast be called on mount and unmount.

To ensure it is called only on mount/unmount, pass an empty array (`[]`) as dependencies.

If the code inside your effect depends on other component props, go read either:
- Combine with useCallback to reduce triggering deps
- Combine with useRef when depending on a prop without triggering effect

#### Call only on mount

You can use an extra ref variable that you update on the first call of your effect.

It works because the change of the ref's value will not trigger any update (that's the point of a ref)

```js
const mounted = useRef(false);

useEffect(
  () => {
    if (mounted.current === false) {
      // do my stuff
    }
    mounted.current = true;
  },
  [mounted],
);
```

> Notice that I pass the ref as a dependency of my effect to ensure I won't have a stale value when the internal function is called.

#### Call only on unmount

Same as before but you reverse your condition inside the effect

```js
const mounted = useRef(false);

useEffect(
  () => {
    if (mounted.current === true) {
      // do my stuff
    }
    mounted.current = true;
  },
  [mounted],
);
```

### Call only on update

See [docs](https://reactjs.org/docs/hooks-faq.html#can-i-run-an-effect-only-on-updates)

#### Only on update (+unmount)

It is the same as "Call only on unmount"

```js
const mounted = useRef(false);
const [dep, setDep] = useState(null);

useEffect(
  () => {
    if (mounted.current === true) {
      // do my stuff
    }
    mounted.current = true;
  },
  [mounted, dep],
);
```

#### Only on update, enforcing not on unmount

Use another extra ref, which will hold your deps previous values and trigger only if they changed

```js
const mounted = useRef(false);
const [dep, setDep] = useState(null);
const depRef = useRef(dep);

useEffect(
  () => {
    if (mounted.current === true && depRef.current !== dep) {
      // do my stuff
    }
    depRef.current = dep;
    mounted.current = true;
  },
  [mounted, dep, depRef],
);
```

### Combine with useCallback to reduce triggering deps

```js
const onLoad = useCallback(
  () => {
    loadA();
    loadB();
    loadC();
    if (d.ok) {
      doD();
    }
  },
  [loadA, loadB, loadC, d, doD],
);

const mountEffect = useEffect(onLoad, []);
```

### Combine with useRef when depending on a prop without triggering effect

```js
const nameRef = useRef('titi');

const onClick = useCallback(
  () => {
    nameRef.current = 'toto';
  },
  [nameRef],
);

const mountEffect = useEffect(
  () => {
    console.log(`hey ${nameRef.current}`);
  },
  [nameRef],
);
```
In this example, console will only output "hey titi".


## UseState

Try to always separate independent state variables

> [docs](https://reactjs.org/docs/hooks-faq.html#should-i-use-one-or-many-state-variables)

Remember, in a functional component, updating a state variable triggers:
* a re-render of your component
* a recomputation of all your dependent hooks
* a recomputation of all non-memoized code.
