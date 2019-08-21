# Introduction

Here are defined template of meetings we do to organize our sprints.

We use kind of SCRUM to organize the project. We do not consider applying fully SCRUM is a good idea or even a goal.
We consider being able to take advantage of SCRUM and remove some strictnesss if not applicable to our workflow, team...

**We consider Agile over SCRUM: Individuals and interactions over processes and tools**

## What is a sprint:
A sprint is an iteration of our product and our processes.
At the end of sprint, a new version can be released and deployed on production. This new version contains new features, improvements, bug fixes...

### Why do we do agile method ?
Agile is meant to leave technical decisions to the technical people.

12 principles in [Agile Software Manifesto](https://agilemanifesto.org/principles.html) reflects quite well Misakey's philosophy:
- self-organized teams
- flexible requirements
- continuous delivery
- simplicity

_____
# Sprint Review
_The goal of a Sprint Review is to summarize what has been done or reported during the sprint. Here We talk here about functional progress and rarely technical according to the audience. It happens at the end of a sprint._

Type of attendees: Misakey Product/Technical Team, Internal/External Stakeholders...

Technical/Feature teams should express turn by turn:
## Step 1: Objectives reminder
We remind what was the initial objectives of the sprint.

## Step 2: What has been accomplished (macro)
What has been done during this sprint - we talk here about issues that have been closed.
What has been done additionally to what has been initially defined.

## Step 3: What had not been done (micro)
What has been not done during the sprint, the why (time, deprioritized...), or how far the task is reported in the future.

## Step 4: Demo
Demo should be prepared in advance before the sprint planning. All what is shown in demo is available on production with next release.

_____
# Sprint Retrospective
_The goal of a Sprint Retrospective is to summarize good and bad things that occurred during the sprint. Here we discuss about individual and team feedback about internal process, project state...  It happens at the end of a sprint._

Type of attendees: Misakey Product/Techincal Team.

## Step 1: Previous action plans
Check previous action plans have been done, if not discuss about it and its potential postpone.

## Step 2: Writing down
Everyone write on post-its, into 4 categories:
* Happy
* Sad
* Frustrated
* Questions / Facts

## Step 3: Presentation
Everyone presents its Post-its one by one.
We don't comment it, ask questions or give feedback about it. It will be done if the post-its receive a certain amount of vote later.

## Step 4: Answer questions
Answer to every facts/questions asked in step 2.

## Step 5: Votes
Everyone can vote for up to 3 post-its they want to discuss/highlight.

## Step 6: Discussion
We talk more in details about post-its with the highest number of votes within the remaining time.
Either people who voted for it asks questions about it, either people who did write the post-its elaborate, or both.

The output of this discussion is in general one or many action plans. Each action plan should have someone responsible for it and reported at each retrospective if not done.
Sometimes, we don't need action plans since the post-it is just a fact and don't need to necessary have a follow-up.

## Step 7: Next Sprint objectives
We share the objectives of next sprint, corresponding most of the time to specifications.
Everyone should have access to the list of specifications that must be done during next sprint after the retrospective, in order to prepare the Sprint Planning.

_____
# Sprint Planning
_The goal of a Sprint Planning is to prepare the current sprint correctly. It happens just before a sprint starts. After this meeting has been done, we have the list of all tasks that must be done during the sprint, we know team needs/dependencies, priority of tasks, how a task is difficult or long. The goal of this meeting is to limit interactions during sprint such as: how the feature should be built, how to solve technically this things..._

Type of attendees: Misakey Team.

## Step 1: Homework (to do before the Sprint Planning)
Everyone split specifications into small technical tasks on corresponding projects. Specifications should be challenged to be sure we have all functional information to work on features.
So the team creates issue, tag them, design them.
Align technical implementation with product vision if necessary.

## Step 2: Facts presentation (start of Sprint Planning meeting)
* Holidays/Days off
* Important events during the sprint (MEP, new client...)

## Step 3: Priorities and dependencies
* What is the priority for the sprint (must be done/delivered first)
* What are the need from a team to another team during the sprint (to prioritize correctly tasks)

## Step 4: Estimations (we split ourselves into technical teams to estimate tasks)
One by one we take our issues, present it, then one by one and everyone vote on the weight.
Weight is a mix between complexity and time.
You can weight only using the Fibonacci suite (1, 2, 3, 5, 8, 13, 21...) a task with a weight a 21 should certainly by split into small tasks, or have a task to prepare correctly that one.

## Step 5: Consideration
We consider after the estimation if all tasks are going to be done or not during the sprint. We can remove and prioritize some against others.

_____
# Sprint Refinement
_The goal of a Sprint Refinement is to prepare the next sprint correctly. It happens in the middle of a sprint. After this meeting has been done: everyone should aware of the next sprint scope, we have insights about feasibility of features. It is the moment we define required specifications to correctly answer the business needs._

Type of attendees: Misakey Team.

## Step 1:
Define what is current Sprint state and what is the vision about feasibility of the current sprint tasks.

## Step 2:
Our biggest items are mock-ups: split them into specifications.
We should split these mock-ups after having running through it into specifications issues.

## Step 3:
Do really quick analysis of specifications to understand the subject.
Do high estimate specifications. And consider what could be done in next sprint.
Identify what does lack functional or technical specification.

## Step 4:
Identify strongly-related items that imply:
- shared work: expertise, knowledge sharing.
- synchronization.
