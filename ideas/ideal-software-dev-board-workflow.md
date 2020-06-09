## My ideal software development board workflow

- [My ideal software development board workflow](#my-ideal-software-development-board-workflow)

### Columns

1. Incoming
2. In Progress
3. Peer Review
4. Ready to Promote
5. In QA
6. In Stage
7. UX Acceptance
8. Done

#### Brief column descriptions

- [Incoming](#incoming): All tickets in a sprint start here
- [In Progress](#in-progress): Dev work has been started but is not finished
- [UX Acceptance](#ux-acceptance): Tickets that are waiting for UX signoff
- [Peer Review](#peer-review): Tickets that are waiting for dev peer review
- [Ready to Promote](#ready-to-promote): Tickets that are reviewed and
- [In `{ENV}`](#in-env): Tickets that have been deployed to `{ENV}`
- [Done](#done): Tickets are done and ready to deploy to prod! 🚀 🎉

### Labels

1. `blocked` (red)
2. `dev-approved` (green)
3. (`qa` | `stage`)`-tested` (green)
4. `ux-approved` (green) | `ux-changes-requested` (red)

Labels represent a cumulative record of "what got done", something we can audit
when something goes wrong to provide feedback on our workflow.

- If a ticket is not labelled `blocked` it is considered in progress (i.e. no
  `in-progress` label is necessary, as that is the default state)
- If a ticket has not been `dev-` or `ux-approved`, or `[...]-tested`, it is
  considered unreviewed and untested. Therefore, no labels for the negative
  states are necessary.

### Workflow

In general, tickets move left to right only. This protects certain columns from
abuse or becoming "dumping grounds". It also helps tickets reflect their "true"
progress through the workflow.

#### Incoming

All tickets start in "Incoming" at the beginning of the sprint.

#### In Progress

When a dev begins work on a ticket, they move it from "Incoming" to "In
Progress" and assign the ticket to theirself. They are now the ticket's "primary
caretaker" and responsible for carrying it through the rest of the workflow.

If the ticket becomes blocked, the assignee adds the `blocked` label (red) to
signify its status. This helps call out tickets that might need attention or
help. Once a ticket is unblocked, the label is removed.

When dev work is completed, the assigned dev moves the ticket to "UX
Acceptance".

#### UX Acceptance

In this column, the UX designer reviews the work.

If the work doesn't meet the design requirements, the UX designer adds the label
`ux-changes-requested` (red). The dev and designer work out the details of the
necessary changes and decide whether to leave the ticket in this column or move
it back to "In Progress".

Otherwise, if the ticket work does meet design requirements, the UX designer
adds the `ux-approved` label (green). This signifies to the dev that the ticket
is ready to move to "Peer Review".

#### Peer Review

During this step in the tickets lifecycle, another dev reviews code changes/PR
and tests the implemented features for "functional correctness". If changes are
requested before approval, the ticket remains in "Peer Review" while the changes
are made.

When another dev has fully reviewed the code and functional correctness of the
work, they add the `dev-approved` label (green) to the ticket. The assigned dev
then moves the ticket to "Ready to Promote".

#### Ready to Promote

Here, the ticket work is ready to be promoted to QA for testing. In this column,
the dev makes whatever additional preparation is needed (setting up Akkeris
apps, pipelines, etc) for promoting the app to QA, stage, and prod.

Once completed, the dev promotes the changes to QA and moves the ticket to the
"In QA" column.

#### In `{ENV}`

This indicates column that the ticket is ready for testing in the QA
environment. The dev remains the primary assignee for the ticket; the SET who
will test the ticket adds theirself as a secondard assignee.

In these columns, the SET completes all necessary testing and test development
work for the given encironment. If testing results in additional dev changes
that must be made, a conversation about moving the ticket back to the dev's "In
Progress" column takes place, if necessary.

When a ticket passes all of the testing in `{ENV}`, the SET adds the label
`{env}-passed` (green). This signifies to the dev that the ticket is ready to be
promoted to the next environment. The dev completes the necessary steps for
promotion, and moves the ticket to the next column.

(This repeats from "In QA" to "In Stage".)

#### Done

Once a ticket is promoted and tested in both QA and Stage, and labelled `qa-`
and `stage-passed`, it's done and ready to deploy to prod! Hooray! 🥳

### Additional considerations

#### Alternative names

- "Incoming" could instead be named "To Do"

#### Working agreements

- Let's consider a new working agreement to limit the amount of work in the "In
  Progress" column (as much as possible). This will help keep clear what
  features are meaningfully "underway" and also make sure we're working in an
  incremental, iterative fashion and making steady progress.

---

[#ideas](index.md) #software-development #process #workflow #original-content
