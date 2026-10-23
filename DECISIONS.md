# Decision Log

Each entry records a significant choice, who owned it, the alternatives we rejected, and
why. Newest entries go at the bottom. Entries are never deleted; a reversed decision gets
a new entry that references the old one.

Template:

```
## D-XXX: <title>
- Date:
- Owner:
- Status: proposed | accepted | superseded by D-YYY
- Context:
- Decision:
- Alternatives considered:
- Consequences / how we'll know if this was wrong:
```

---

## D-001: Project topic — decisions lost in LINE group chats

- Date: 2026-10-24
- Owner: Sean-Fang178 (proposal); team to ratify at next sync
- Status: proposed
- Context: CP1 requires a real collaboration pain point that we can validate with external
  users before Week 8. Every member has experienced student group projects coordinated
  almost entirely in LINE.
- Decision: Build a tool that turns an exported LINE chat into a list of candidate
  decisions and action items, which the people involved must confirm before they count.
- Alternatives considered:
  - *Group-project contribution tracker (free-rider visibility)* — rejected: interviewees
    are unlikely to speak candidly about teammates, and fair evaluation is hard to design.
  - *PR review assistant for student teams* — rejected: overlaps with this course's own
    tooling, and few external interviewees use GitHub for team work.
- Consequences / how we'll know if this was wrong: if fewer than half of our interviewees
  report missing or misremembering a group decision in the past semester, the problem is
  not as common as we assume and we revisit the topic.

## D-002: AI proposes, humans confirm

- Date: 2026-10-24
- Owner: Sean-Fang178 (proposal); team to ratify
- Status: proposed
- Context: An LLM can extract decisions from chat text, but a wrong "decision" that people
  trust is worse than no list at all.
- Decision: The model only produces *candidates*, each linked to its source messages.
  A candidate becomes part of the shared list only after the assigned owner (or, for a
  group decision, a second member) confirms it. The model never assigns owners that are
  not named in the chat.
- Alternatives considered:
  - *Fully automatic summary* — rejected: no accountability, and errors are silent.
  - *No AI, manual entry only* — kept as the baseline condition in our evaluation, so we
    can show whether the AI step actually adds value.
- Consequences / how we'll know if this was wrong: if users confirm >95% of candidates
  without opening the source messages, confirmation has become rubber-stamping and we
  need a different checkpoint design.
