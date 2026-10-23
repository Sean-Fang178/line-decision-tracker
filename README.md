# LINE Decision Tracker

CSIC30216 Fall 2026 — Final Project, Group 15.

Student teams make decisions in LINE group chats, and those decisions get buried under
hundreds of messages. This tool takes an exported LINE chat (`.txt`), proposes candidate
**decisions** and **action items (owner / deadline)** with links back to the source
messages, and asks the named people to **confirm or dispute** each item. Only confirmed
items enter the team's shared decision list.

> Status: Discovery phase (CP1). No application code yet.

## Repository conventions

- `main` is protected: all changes land through a pull request with at least one approving
  review from the current code steward. Direct pushes are blocked.
- Every PR uses [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md).
- Significant choices (and the alternatives we rejected) are logged in
  [`DECISIONS.md`](DECISIONS.md).
- CP1 write-up: [`docs/CP1.md`](docs/CP1.md).

## Code steward

The code steward reviews and approves PRs into `main`. The role rotates every two weeks;
each member serves at least twice before CP3.

| Period | Code steward |
|--------|--------------|
| Week 7 – Week 8 (current) | Sean-Fang178 |
| Week 9 – Week 10 | _Member B_ |
| Week 11 – Week 12 | _Member C_ |
| Week 13 – Week 14 | _Member D_ |
| Week 15 – Week 16 | rotation repeats |

When the steward rotates, update this table in a PR and add a line to `DECISIONS.md`.
