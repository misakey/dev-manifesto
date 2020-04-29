# Practices
Frontend team practices regarding organization, development, review, communication, release

## Introductory notes

This document describes frontend team practices as part of Misakey practices, workflow and lifecycle.

Please refer to appropriate documentation for more information on them.

Terms mentioned in this document:
- User Need => UN
- Product Need => PN
- Technical Design
- Merge Request => MR
- Review
- Issue
- Slider


## Table of Contents
* [Organization](#organization)
* [Development](#development)
* [Review](#review)
* [Release](#release)

## Organization

### Technical design of Product Needs

Technical design does not require the whole frontend team to study, design and write a technical design material.

However, the whole frontend team must be involved to review and validate the technical design material.

In good cooperation, any member of the team is legitimate to ask for others' help via [Team communication](#team-communication) when facing risk during writing of the technical design material.

### [Frontend Slider](https://gitlab.misakey.dev/misakey/product-needs/issues/387)

On slider issues with high complexity `>=★★★☆☆`, members must at least validate via [Team communication](#team-communication) information were already shared or written inside the issue.

In case of architectural design requirements, it is up to the developer to ask for team, if they feel the need, via [Team communication](#team-communication)

On slider issues with lower complexity `<=★★☆☆☆`, architectural considerations should be minor. 

If there are any, they could be discussed during code review.

It is important that both developers and reviewers make sure their review is constructive on such occurrences.

### Refactoring code: when, how ?

It is fine to refactor code during dev, but be careful not to add too much workload to your development and to reviewers.

Keep priorities in mind.

When you spot something that would require a refactor, you are able to estimate its importance and priority over your current developments.

- Can you skip it now, without impacting your current development ?
- Can you refactor quickly and efficiently ? 
- Is it closely related to your current tasks ? 
  - you can add a trail of flowers for later
- Whenever you choose not to implement that refactor, simply create a slider issue for later


### Team communication

We use Mattermost channels as a ground for short term talks and questions.

There is a channel dedicated only to talks between frontend team members:
- [frontend team](https://chat.misakey.dev/misakey/channels/frontend-team)

There is a channel to discuss frontend subjects with the rest of the Misakey team, be it issues, bugs, questions, etc: 
- [frontend](https://chat.misakey.dev/misakey/channels/frontend)

Prefer team communication over one-to-one when you need help, so that everyone can collaborate harmoniously.

## Development


### File and folder architecture

#### Packages

We want to keep packages and put stable, reusable and generic code in them.

For now, being stable, reusable and generic in the context of Misakey frontend project(s) is enough.

All team members are equally responsible to refactor project - whenever appropriate - move code towards packages when it matches those rules.

##### UI package

We want to pay attention to what is put in misakey/ui package: only components following [package rules](#packages), with minimal external dependencies

#### Components splitting

##### Split components for readability

It is perfectly fine to split code into multiple subcomponents locally to achieve more readability.

It is perfectly fine to leave them as is, next to their consuming component.

Thinking about their reusability is an optional following step.

Make sure to apply [proper rules](#reusable-components) when refactoring these components into reusable ones.

##### Reusable components

Reusable components should be stored in dedicated folders, unrelated to where they are consumed.

There are three possible places to keep such components, ordered by priority.

###### 1. misakey/ui components

When components follow [ui package rules](#ui-package)

They should be put in the package `misakey/ui/[path]`.

###### 2. Dumb components

Components holding no logic related to the external world.

They are only presentational: no API call, not connected to store, can have translations.

###### 3. Smart components

Components holding logic.

### Naming rules

Ensure **component** names are more or less their path in project.

Ensure names of **variables**, **functions**, **components** bring meaning regarding what they do.

Ensure **factories**, **functions** and **values** are easy to distinguish: 

```js
const getToto = makeGetToto(); // factory => function

const toto = getToto(); // function => value
```

Name **booleans** with prefix `is`.

Name **hooks** with prefix `use`.

#### API action builders

In code, to shorten API building, we often wrap it inside **helper functions**.

To avoid having 2 very similar names with no uniformity between **callback** and **helper**:
- name the **helper** constructor `HttpVerbActionBuilder` => `getDataboxBuilder`
- name the result of `useCallback` `HttpVerbAction` => `getDatabox`


## Review

### When should we validate respect of dev practices

If code is not understandable enough.

If it's the level of a proper naming forgotten, not important.

If it seldom happens, deal with it. 

If it's recurring, feel free to ask for a talk.

### Goals of our reviews

- Deliver clean code, with few bugs
- Share vision on codebase

### Not goals of our reviews

- Have a 100% uniform code
- Implement exactly what a reviewer would have done

### Towards less code review

#### As a developer

Be more explicit on code and what could / should be reviewed in code.

Bring knowledge about code and changes.

Bring as much knowledge as possible towards functional tests.

#### As a reviewer

Put focus on functional tests and bug hunt with them, rather than trying to understand everything in code.

Distinguish reading code and reviewing code.

Read code.

Be less difficult when reviewing code.

Approvals should be given more easily via [emoji](#emoji).

### Emoji

- :zap: (`:zap:`) "You do not need to ping me back if you implement with my proposal"
- :see_no_evil: (`:see_no_evil:`) "I am not sure of what I propose, if I'm wrong, you can skip"

## Released code

### QA and QA issues

Always remember the main goal is QA efficiency.

#### Prioritizing / Postponing phase

Frontend team can either elect a single member or gather to handle this phase.

However, once ordering is done, it has to be validated by the whole frontend team.

#### Assignment, clearing

Assign yourself issues one by one so that we can all share charge of solving them.

In good cooperation, there are cases where it is worth grouping issues in a single MR.

Being assigned to a QA issue means you are currently working on it. 

Deassign yourself from QA issues if you are not currently working on them.

Feel free to ask for help via [Team communication](#team-communication) if you need help to solve an issue.

Remember, the main goal is QA efficiency.

### Hotfixes

You can ask for explicit assignment on a hotfix via [Team communication](#team-communication).

Sometimes we only need a few team members to work on a hotfix. Sometimes help is welcome.

### Creating / Updating slider or bug issues

When a slider issue is not ready for someone else to work on it, add labels:
- Todo
- Draft

Ping people who have knowledge inside issue (ex: followup issues).

Regularly clean slider issues, particularly your drafts whenever you have time.

### Sentry issues

#### Future work

There are studies to handle to see how we could improve our management of sentry issues.

#### For now

Assign yourself on Sentry issues you checked or are currently checking.

We consider an issue is handled as long as someone is assigned to it.