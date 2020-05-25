# Our level of expectation

Those rules has been written in a context of exploration of a Product Market Fit.

## "Move fast break things" vs "stability"

- We want to produce something functional. We are okay with having imperfect UX or some non-managed edge case.
- Still, it's important to be clean in what we design, at least for core production.
- We want to avoid over-engineering, we want to get usage more than theory.

## QA / Betatesting

- We want to create automated test for critical and stable blocs
- We don't talk about QA anymore, but about **Betatest**
- Our Betatest are not describe by detailed scenarios, but some global objectives to encourage creativity of the tester
- We have a fixed Betatest manager. Here some recommendation for them:
  - Define a small group for each Betatest (2/3 people)
  - If you involve some dev, take some that didn't produce much feature in the tested scope
  - Try to make the Betatest synchronous (same room, or at least on Mumble)
  - Include product people in Betatest. Try at least one, try with only product people
  - Do not test the whole app on every Betatest
- Be more exhaustive on MR tests (the tester, not the developer), at least on critical subjects, to be more relaxed about having a lighter Betatest

## Review

- It's important to have space to explain what is not understood
- Avoid the mindset "I wouldn't have done that this way", but search more for knowledge sharing or evolution proposition (and make it explicit that it's not blocking)
- Ask yourself if your comment is useful before posting it
- The review is more about testing the functionality than checking the form
- Make explicit in the MR description what do we need from reviewers (what to check, what is not important, where do we need challenge over implementation)
- On trivial cases (small bugfix, translation, tooling), it's okay to bypass the standard review process (you can ask for only one reviewer, or no reviewer at all), if you think it's not dangerous
- Make the review feedback organically improved
- We have a tacit concept of referent on some subject (people having more knowledge on the subject, and on which we can rely to have technical answer)  

## Technical design

- On technical design review, don't think it back from scratch, but check that everything is in order and covered (and as for code review: ban the "I would have done that differently)
- Don't forget a design step before technical decision
- Replace "Functional design" by "Feature design"
  - Done by a feature team (1 front, 1 back, 1 product)
  - Letting the technical restrictions guide the functional design
  - The feature team could ask for expertise / review to other people if required
  - There will still have a technical design after
  - No need for a systematic collective review: the feature team decide who is relevant to review
- Apply the "Less is more" logic to the design and review

