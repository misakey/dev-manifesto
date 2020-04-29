# Refactor Cheatsheet

Here you can find good practice recommendations regarding development of reusable features and refactor.

## How to develop and structure reusable code

### Why creating reusable code ?

- To build bricks, blocks or boxes holding their own logic internally
- To store behaviours as part of reusable objects
- To build features brick by brick

### What is the goal of a reusable code ?

- Integrate components from other libs into our graphical chart
- Implement a closed set of features as part of a reusable brick
- Create variants of an existing component's behaviour.
- Create solid ground for an existing behaviour

### Places to implement reusable behaviours

There are different layers of reusability, each with their pros/cons. I will not argue about that here, but simply propose recommendations.

#### UI

1. theme: for generic visuals on a component, graphical chart
2. component styles: for specific visuals for a component

#### Computation / Logic

1. helper
2. hook: when you need to call other hooks
3. HOC: when depending on UX

#### Data

1. selector: when related to store
2. helper
3. hook: when related to UX
4. HOC: when mixing store, UX

#### Configuration

1. constant: if it is unconditionned
2. helper: when there are conditions

### Reusability vs Complexity => Composition

The more a component extends its behaviour to integrate new uses, the more its complexity grows.

In React, it is very easy to combine and compose multiple sets of features from multiple bricks.

This is why I highly recommend to keep reusable components as small bricks with only a restricted set of features.

Adding extra features is then a matter of composition:
- A does one feature
- B uses A to handle that feature, and adds other stuff

If B needs to interact with how A does its feature, it can easily with such structure.

Keep it simple.

### What not to do when building reusable components

#### Over-engineering 

Do not implement for the future.

Focus on what you need for now. 

Simplicity always gives more possibilities.

#### God object

Do not build god objects.

They can become a mess when they're used everywhere.

Building variants helps handling very close, but still different use cases.

Keep it simple.