# New Yearbook Dev board workflow proposal

- [Columns](#columns)
- [Labels](#labels)
- [Workflow](#workflow)
- [Additional considerations](#additional-considerations)

## Columns

1. Incoming
2. In Progress
3. Peer Review
4. UX Acceptance
5. Ready to Promote
6. In QA
7. In Stage
8. In Prod (Done)

#### Brief column descriptions

- [Incoming](#incoming): All tickets in a sprint start here
- [In Progress](#in-progress): Dev work has been started but is not finished
- [Peer Review](#peer-review): Tickets that are waiting for dev peer review
- [UX Acceptance](#ux-acceptance): Tickets that are waiting for UX signoff
- [Ready to Promote](#ready-to-promote): Tickets that are reviewed and
- [In `{ENV}`](#in-env): Tickets that have been deployed to `{ENV}`
- [In Prod (Done)](#in-prod): Tickets are done once they make it to prod! 🚀 🎉

## Labels

1. `blocked`
2. `dev-approved`
3. `ux-approved`
4. (`qa` | `stage`)`-tested`

Labels represent a cumulative record of "what got done". They should be
primarily additive (not subtractive); in particular, the number of labels which
are in alternation (one must be removed before another is applied) should be
limited.

- If a ticket is not labelled `blocked` it is considered in progress (i.e. no
  `in-progress` label is necessary, as that is the default state)
- If a ticket has not been `dev-` or `ux-approved`, or `[...]-tested`, it is
  considered unreviewed and untested. Therefore, no labels for the negative
  states are necessary.

## Workflow

In general, tickets should move left to right only. This protects certain
columns from abuse or becoming "dumping grounds". It also helps tickets reflect
their "true" progress through the workflow.

#### Incoming

All tickets start in "Incoming" at the beginning of the sprint.

#### In Progress

When a dev begins work on a ticket, they move it from "Incoming" to "In
Progress" and assign the ticket to themselves. They are now the ticket's
"primary caretaker" and responsible for carrying it through the rest of the
workflow.

If the ticket becomes blocked, the assignee should add the `blocked` label (red)
to signify its status. This helps call out tickets that might need attention or
help. Once a ticket is unblocked, the label should be removed.

When dev work is completed, the ticket moves to "Peer Review".

#### Peer Review

During this step in the tickets lifecycle, another dev should review code
changes/PR and test the implemented features for "functional correctness". If
changes are requested before approval, the ticket should remain in "Peer Review"
while the changes are made.

When another dev has fully reviewed the code and functional correctness of the
work, they can add the `dev-approved` label to the ticket and move the ticket to
"UX Acceptance".

#### UX Acceptance

In this column, the UX designer can review the work. If it meets design
requirements, the UX designer should add the `ux-approved` label and then move
the ticket to "Ready to Promote".

#### Ready to Promote

When a ticket has been labelled both `dev-approved` and `ux-approved` it is
ready to be promoted to QA for testing. In this column, the dev makes whatever
additional preparation is needed (setting up Akkeris apps, pipelines, etc) for
promoting the app to QA.

Once completed, the dev can promote the changes to QA and move the ticket to the
"In QA" column.

#### In `{ENV}`

Once a dev has deployed the changes to a new environment, the ticket can move to
the next "In `{ENV}`" column. This indicates that the ticket is ready for
testing in that environment.

The dev remains the primary assignee for the ticket; once a SET has joined the
ticket, they should be added as a secondary assignee.

In this column, the SET completes all necessary testing and test development
work. If testing results in additional dev changes that must be made, there can
be a conversation about moving the ticket back to a previous column, if
necessary.

When a ticket passes all of the testing in `{ENV}`, the SET should add the label
`{env}-passed` and advance the ticket to the next "In `{ENV}`" column.

#### In Prod (Done)

Once a ticket makes it to "In Prod", it's done! Hooray 🥳

## Additional considerations

#### Alternative names

- "Incoming" could instead be named "To Do"

#### Working agreements

- Let's consider a new working agreement to limit the amount of work in the "In
  Progress" column (as much as possible). This will help keep clear what
  features are meaningfully "underway" and also make sure we're working in an
  incremental, iterative fashion and making steady progress.

---

[#ideas](index.md) #software-development #process #workflow #original-content
