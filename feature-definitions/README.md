Feature Definitions
===================

Defining the "end" state, which can be tested.

Why use them?
-------------

Often clients and those working for clients (PMs) give the "how" something should be done.  This is because they have or listened to the problem and developed an opinion on "how I would do it".  At this point the "how" is confused with the "why" and in many cases the "why" is forgotten.

When issues arise during later stages of development choices may be made which adhere to the "how", but violate the "why".  So by the time the feature is finished it is useless.


Format for Client - User story
------------------------------

Client / PMs are required to give requests in at least format. or something that can be converted to this format.

`As a <user>, I want <desire> so that <business case>`

or

`In order to <business case> as a <user>, I want <desire>`


Format for testing - Scenarios
------------------------------

This format is one step away from actually testing.  This format is useful if the feature has many stakeholders (many eyes watching) or cost of failure is very high.  If neither of these is the case then develop [acceptance tests](/style#acceptance-tests) directly.

```
Feature: <name>
  <user story>

  Scenario: <testable item>
    <details>
```

### Vision / Happy path

Clients only care about the happy path, or "vision".  So focus on them.

Scenarios like "a user sees an error if..." are only useful if the client actually wants to limit the user.