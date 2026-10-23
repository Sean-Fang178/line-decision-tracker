# Group 15 — Checkpoint 1 (CP1)

**Project:** LINE Decision Tracker
**Course:** CSIC30216 Fall 2026 · **Submitted:** 2026-10-25
**Members:** 王翔麟 (Sean-Fang178) · _Member B_ · _Member C_ · _Member D_
**Repository:** https://github.com/Sean-Fang178/line-decision-tracker

---

## 1. Team Charter

### 1.1 How we decide when we disagree

1. **Default: whoever owns the work item decides**, after hearing objections in the PR or
   chat thread. Small, reversible choices (naming, library for a minor feature, UI copy)
   stop here.
2. **Significant or hard-to-reverse choices** (anything that would get a `DECISIONS.md`
   entry: data model, AI provider, evaluation design, scope cuts) are raised as a short
   written proposal in Discord `#decisions` with at least one alternative. Members have
   **48 hours** to object.
3. **No objection in 48 h → accepted.** With objections, we discuss at the next weekly
   sync. If still split, we take a **majority vote (3 of 4)**. On a 2–2 tie, the
   **current code steward** casts the deciding vote, and the losing side's reasoning is
   recorded under "Alternatives considered" so we can revisit it with evidence later.
4. Evidence beats opinion: if the disagreement is about what users want, the default
   resolution is "ask two users", not "argue longer".

### 1.2 What "done" means

A work item is done only when **all** of the following are observable:

- Its PR is **merged into `main`** with at least one approving review from the code
  steward (or a non-author member if the steward is the author).
- The reviewer could **run it from a fresh clone** following the steps in the PR's
  "How to verify" section.
- Tests for new logic pass in CI (from Week 9 onward, once CI exists).
- If it changes setup or behaviour, the **README is updated in the same PR**.
- If it embodies a significant choice, a **`DECISIONS.md` entry** exists.

For non-code items (interviews, evaluation sessions): done = notes are committed to
`docs/` in the agreed template and one other member has read and commented on them.

### 1.3 Communication norms

| Channel | Used for | Expected response |
|---|---|---|
| Discord server (`#general`, `#decisions`, `#pr-review`) | Day-to-day coordination, decision proposals, review requests | Within **24 h** on weekdays |
| LINE group | Urgent only (blocked, deadline at risk, schedule change) | Within **4 h** during 09:00–23:00 |
| GitHub PR comments | All code discussion; the decision record lives here, not in chat | Steward reviews within **48 h** |
| Weekly sync | 30 min, every **Thursday 21:00** (Discord voice); agenda posted by Wednesday | Attendance expected; absent members read notes within 24 h |

- If a member will be unavailable for more than two days (exams, travel), they post it in
  `#general` in advance.
- Anything decided in voice or LINE is not decided until it is written in `#decisions` or
  a PR. (We are building a tool about exactly this failure; we intend to practice it.)

---

## 2. Problem Statement with Evidence

### 2.1 The problem

University student teams in Taiwan coordinate group projects almost entirely in **LINE
group chats**. Decisions ("we use topic B", "slides due Saturday night") and assignments
("A does the literature part") are made in fast, interleaved conversations mixed with
logistics, jokes and stickers. A busy afternoon produces hundreds of messages.

The specific pain point is: **a team member who was not actively following the chat
cannot reliably reconstruct what was decided and what they are responsible for.**
They scroll back, ask "so what are we doing now?", or guess. The consequences are
duplicated work, missed tasks, and late-stage conflicts over "I thought we agreed…".

**Affected users:** undergraduate and master's students working in 3–6 person course
project teams who coordinate primarily through LINE. Secondary: club and student-
association officers who coordinate events the same way.

### 2.2 Evidence from conversations outside our team

> **[TO BE COMPLETED BEFORE SUBMISSION — real interviews only.]**
> We will conduct at least two 10–15 minute conversations with students outside Group 15
> using the guide in Appendix A, and summarize each below in the template provided.
> No summary is included here until the conversation has actually taken place.

#### Conversation 1

- **Who (role, not name):** _e.g. 3rd-year EE student, 4-person course project_
- **Date / format:** _e.g. 2026-10-24, 12 min, in person_
- **Context:** _how their team coordinates, how many messages per week_
- **Most recent concrete incident:** _what was decided, who missed it, what happened_
- **Current workaround and why it falls short:**
- **Notable quote (paraphrased with permission):**
- **What this tells us / what surprised us:**

#### Conversation 2

- **Who (role, not name):**
- **Date / format:**
- **Context:**
- **Most recent concrete incident:**
- **Current workaround and why it falls short:**
- **Notable quote (paraphrased with permission):**
- **What this tells us / what surprised us:**

#### What we do not know yet

- How often this happens per project. Our own experience suggests several times per
  semester, but that is not evidence.
- Whether students would be willing to export a chat and paste it into a tool at all
  (privacy concerns about the chat contents).

### 2.3 Why current tools and methods fall short

| Current approach | Why it falls short |
|---|---|
| **Scroll back through LINE** | Search only works if you already know the keyword; decisions are spread across many messages and often revised later ("actually let's change to…"). |
| **LINE Notes / Announcements (記事本／公告)** | Requires someone to remember to write it; in practice used for one or two items and quickly goes stale. Nobody confirms they have read or accepted it. |
| **Shared Google Doc / Notion task board** | Separate from where the discussion happens; keeping it in sync is extra work that usually falls on one person, then stops. |
| **Asking the group "what did we decide?"** | Interrupts others, and the answer depends on who replies first; it may itself be wrong. |
| **Pasting the chat into ChatGPT** | Produces a plausible summary with no source links, no owner confirmation, and no shared view; errors go unnoticed and only one person sees it. |

The common gap: **no step where the people involved explicitly agree that "this is what we
decided and this is mine."** Our tool adds that step at low effort.

---

## 3. Initial Interaction Design Sketch

### 3.1 What the tool does

A small web app. A team creates a project space and invites members. Any member uploads
an exported LINE chat segment. The system proposes **candidate items** (decisions and
action items), each linked to the exact messages it came from. The people named in an
item confirm or dispute it. Confirmed items form the team's **shared decision list**,
which is what a member who missed the chat reads instead of scrolling.

### 3.2 Inputs and outputs

**Inputs**

- LINE chat export (`.txt`, LINE's built-in "Export chat history"), optionally limited to
  a date range.
- Team roster: display names in LINE mapped to members of the project space.
- Per-item human actions: *confirm*, *dispute (with a comment)*, *edit*, *mark obsolete*.

**Outputs**

- **Candidate list:** each item has a type (decision / action item), text, owner (only if
  named in the chat), deadline (only if stated), and links to 1–5 source messages.
- **Shared decision list:** confirmed items only, with who confirmed and when.
  Disputed items are shown separately until resolved.
- **"Catch-up" view** for a member: items assigned to them and decisions made since their
  last visit.

### 3.3 How two users collaborate with it

Scenario: Amy and Ben are in a 4-person team. On Tuesday the team discussed in LINE for
two hours; Ben was in lab and did not follow.

1. **Amy** exports Tuesday's chat and uploads it to the project space.
2. The tool proposes five candidates. One reads: *Action — Ben: draft the related-work
   section, due Fri 10/30 (source: 3 messages, 14:02–14:10).*
3. **Ben** opens the catch-up view that evening. He sees that item, clicks the source link
   to read the three messages in context, and **confirms** it.
4. Another candidate reads *Decision: use dataset X*. Ben remembers the team later
   switched to dataset Y in a different thread, so he **disputes** it and adds a comment.
5. **Amy** sees the dispute, checks the later messages, edits the item to dataset Y, and
   **confirms** it. It now appears in the shared list with both names attached.

Neither had to ask "what did we decide?" in the group, and the record shows who agreed
to what.

### 3.4 Where AI is used, and where it is not

| Step | Who decides |
|---|---|
| Finding candidate decisions and action items in the chat | **AI proposes** (LLM extraction) |
| Linking each candidate to source messages | **AI proposes**, shown to the user for checking |
| Whether an item is real and correct | **Human** (owner or second member confirms) |
| Who owns a task | **Human.** The AI may only copy an owner explicitly named in the chat; it never infers one |
| Resolving a dispute | **Humans** in the team |

---

## 4. Draft Evaluation Plan

### 4.1 What success looks like (observable, measurable)

The tool succeeds if **a team member who did not follow a discussion can correctly
identify what was decided and what they are responsible for, faster and more accurately
than by reading the chat**, and if teams keep using it without being reminded.

Primary measures:

- **Recall accuracy:** % of ground-truth decisions and action items (owner + deadline)
  a participant correctly reports after catching up.
- **Catch-up time:** minutes from starting until the participant says they are done.
- **Extraction quality** (for the AI step): precision and recall of candidates against a
  human-labelled ground truth, and the share of AI errors caught by human confirmation.

Secondary measures:

- **Confirmation without reading:** % of items confirmed without opening their source
  messages (a high value is a warning sign of rubber-stamping).
- **Retention** (field study): whether teams upload again in week 2 without prompting.

### 4.2 Target users and recruitment

- **Who:** NYCU undergraduate or master's students currently in a course project team of
  3–6 people that coordinates in LINE. Not members of this course, so they have no stake
  in our grade.
- **How:** personal networks (classmates in other courses, dorm mates, club members);
  posts in department LINE / Discord groups; and the two CP1 interviewees, who we will
  ask to refer their teammates.
- **Target numbers:** 12 individual participants for the controlled study (Study A);
  2 real teams for the field trial (Study B).
- **Incentive:** a drink voucher (about NT$50) per participant, paid by the team.

### 4.3 Method and timeline

**Study A — Structured observation, within-subjects (main evidence)**

- We prepare **two realistic chat logs** (≈300 messages each, from a mock project
  discussion written and role-played by our team, with known ground truth: about 6
  decisions and 8 action items each). We use our own role-played chats rather than real
  ones, so that no participant's private messages are needed.
- Each participant plays a team member who missed the discussion and catches up on one
  log by **reading the raw chat (baseline)** and on the other **using the tool**. The
  order of conditions and logs is counterbalanced.
- After each condition: a 10-question recall quiz (who / what / when) and the catch-up
  time. After both: a 5-minute interview on trust and effort.
- We observe and note where they hesitate, re-read, or distrust an item.

**Study B — Field trial (does it survive real use?)**

- Two real student teams use the tool for **two weeks** on their own projects.
- Pre/post survey (5 items, 1–5 scale): "I know what our team has decided" and "I know
  what I am responsible for", plus a count of "what did we decide?" messages in their
  chat before and during the trial (self-reported by the team, no message content
  collected).
- Exit interview with one member per team.

| Week | Activity |
|---|---|
| 7–8 | CP1 interviews (≥2), refine problem statement; write mock chat logs and ground truth |
| 9 | Walking skeleton: upload → candidates → confirm |
| 10 | Pilot Study A with 2 participants; fix the protocol |
| 11 | Study A with remaining participants (target 12) |
| 12 | Recruit Study B teams; CP2 |
| 12–14 | Study B field trial (2 weeks) |
| 14–15 | Analysis, write-up; CP3 |

### 4.4 Evidence that would convince a skeptic

We will consider the tool successful only if **all** hold in Study A (n ≥ 12):

1. Mean recall accuracy with the tool is **at least 15 percentage points higher** than
   the baseline, and at least **9 of 12** participants individually score higher with the
   tool.
2. Median catch-up time with the tool is **at most half** of the baseline.
3. AI extraction on our two logs reaches **≥ 80% recall** of ground-truth items; and in
   the confirmation step, participants **catch at least half** of the deliberately
   ambiguous or wrong candidates, rather than confirming them.

And in Study B: at least **one of two teams uploads a second time unprompted**.

If the results fall short, we will report them as they are. In particular, if the
baseline already scores high (above 85%), our premise that people cannot reconstruct
decisions is wrong for this population, and we will say so.

### 4.5 Human–AI decision boundary

- The AI **never** creates an item that appears in the shared list without human
  confirmation.
- The AI **never** assigns an owner or deadline that is not explicitly present in the
  source messages.
- Every AI-proposed item shows its source messages; users can always check.
- To test whether the AI step adds value, Study A will include a **manual-entry
  variant** for a subset of participants if time allows. If people do equally well
  writing items themselves, we will drop or reduce the AI component (logged in
  `DECISIONS.md`).
- Privacy: in Study B, uploaded chats stay on our server only for the trial period and
  are deleted afterwards. Chats are sent to the LLM provider only with the team's explicit
  consent, and we will state this in the consent form.

---

## 5. Repository Setup

Repository: **https://github.com/Sean-Fang178/line-decision-tracker**

| Requirement | Status |
|---|---|
| Branch protection on `main` (PR required, 1 approving review, no force-push / deletion) | ✅ |
| PR template at `.github/PULL_REQUEST_TEMPLATE.md` | ✅ |
| `DECISIONS.md` with at least one entry | ✅ D-001 (topic), D-002 (AI proposes, humans confirm) |
| Current code steward documented | ✅ README → "Code steward": **Sean-Fang178**, Weeks 7–8; rotates every two weeks |

---

## Appendix A — Interview guide (10–15 min)

Opening: "We're designing a tool for student group projects. There are no right answers.
We're interested in what actually happened, not what should happen. May I take notes?
I won't record your name."

1. Tell me about a group project you're in this semester. How many people, and where do
   you mostly discuss things?
2. Roughly how active is the chat? How often do you read every message, and how often do
   you skim or skip?
3. **Think of the last time** you weren't following the chat and later needed to know what
   was decided. What happened? (Probe: what did you do, how long did it take, and was
   your understanding correct?)
4. Has the team ever had a misunderstanding about a decision or about who was doing
   what? Walk me through it.
5. Do you use anything besides the chat to keep track: LINE notes, announcements, a
   shared doc, a task board? Does it get kept up to date? By whom?
6. If someone handed you a list of "what was decided and who's doing what" after a long
   discussion, what would make you trust it, and what would make you not trust it?
7. How would you feel about exporting your team's chat into a tool to generate that list?
8. Is there anything about coordinating group work that annoys you more than this?

Close: thank them; ask if a teammate would also be willing to talk; ask permission to
contact them for testing in Week 10–11.

**Note-taking rule:** record concrete incidents and their own words. Do not record
names or chat content they did not choose to share.
