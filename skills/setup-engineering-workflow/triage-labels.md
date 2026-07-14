# Triage Labels

The skills speak in terms of five canonical triage roles plus one completion label. This file maps those roles to the actual label strings used in this repo's issue tracker.

| Canonical workflow role | Label in our tracker | Meaning                                  |
| -------------------------- | -------------------- | ---------------------------------------- |
| `needs-triage`             | `needs-triage`       | Maintainer needs to evaluate this issue  |
| `needs-info`               | `needs-info`         | Waiting on reporter for more information |
| `ready-for-agent`          | `ready-for-agent`    | Fully specified, ready for an AFK agent  |
| `ready-for-human`          | `ready-for-human`    | Requires human implementation            |
| `wontfix`                  | `wontfix`            | Will not be actioned                     |
| `completed`                | `completed`          | Implemented, finalized, and closed       |

When a skill mentions a role (e.g. "apply the AFK-ready triage label"), use the corresponding label string from this table.

When `deliver-ticket` finalizes a ticket, remove the `ready-for-agent` label and add `completed` before or when closing the ticket.

Edit the right-hand column to match whatever vocabulary you actually use.
