# C5 — Interaction Discipline: Gates, Modes & Never Vibe Code

> **Module:** C5 · **Track:** Shared Core (all roles) · **Time:** ~75 min · **Format:** 📖 Read + 🧪 Hands-on + ✅ Graded
> **Prerequisites:** [C4 — Scopes, depth & inputs](C4-scopes-and-inputs.md)

## Learning objectives

By the end of this lesson you can:

- Use the three **interaction modes** (Guide Me / Edit File / Chat) and know when each fits.
- Work an **approval gate**: approve, request changes, or (as an escape hatch) accept-as-is.
- Explain the **human-turn safeguard** and why it makes "autopilot approval" impossible.
- Handle the **walking skeleton + ladder prompt** and keep context healthy across **compaction**.
- Apply the cardinal rule: **never vibe code.**

## Why this matters

This is the lesson that separates AI-DLC done well from AI-DLC done dangerously. The whole method's quality claim rests on *humans reading and deciding at gates*. Skip that and you've just automated the production of plausible-looking mistakes. Everything here is a habit, and habits are built by practice — so this module is **graded**.

## Read

### Talking to a stage: three modes, one record

When a stage needs your input, it offers three ways to give it:

```
▸ Choose interaction mode:
  (1) Guide Me — agent asks structured questions
  (2) Edit File — write directly to the artifact
  (3) Chat — freeform discussion
```

- **Guide Me** — the agent leads, asking questions one at a time or in batches. Best when you want to be sure nothing's missed.
- **Edit File** — the agent opens a *questions file* with blank answer fields; you fill it in at your own pace. Best when you already know what you want.
- **Chat** — freeform exploration; the agent extracts decisions and writes them back. Best when requirements are still fuzzy.

All three **converge on the same questions file** as the canonical record, and you can **switch modes mid-stage** without losing captured answers. The file matters: it's the durable, auditable trace of every decision — great for a team where different people answer different questions.

### The approval gate

Every stage except the three Initialization stages ends at a gate:

```
▸ How would you like to proceed?
  (1) Approve — Continue to [next stage]
  (2) Request Changes — Provide revision feedback
```

- **Approve** → the engine marks the stage complete, updates `aidlc-state.md`, shows a progress line (N/total), and advances. The prompt shows the *actual* next stage, computed by the engine — not a guess.
- **Request Changes** → you give specific feedback; the agent revises and re-presents the gate.

Two more options appear in context:

- **Accept-as-is (escape hatch)** — becomes available once you've gone around the revision loop enough (after the 2nd revision you're warned it's coming; from the 3rd cycle it's offered). It approves the current artifact even if imperfect, so a stubborn stage can't trap you.
- **Add Skipped Stage** — during Ideation/Inception, pull a stage the scope skipped back into the plan.

### Why you can't fake an approval

Here's the mechanism that enforces the whole philosophy: **approving requires a real human turn.** Typing a prompt or answering the gate widget records a `HUMAN_TURN` event in the audit ledger, and the engine **refuses an approval unless a human turn was recorded since the last gate** was resolved. A model running on autopilot literally cannot fabricate an approval — someone has to act. (On a harness whose widget doesn't register a turn, type a short "approve" once so it's on record.)

That safeguard is the technical backbone of the cultural rule.

### Never vibe code

**"Vibe coding"** is approving because it *looks* right, without reading the artifact. It's the fastest way to poison a run: an unread error in a requirements doc gets baked into design, code, and tests, and you find it three stages downstream — or in production. Recall the C1 framing: **gates are a loss function.** Their entire job is to catch mistakes early, and they only work if you actually read before you approve.

Practical habits:

- Open and read the artifact (in its record dir) *before* touching the gate.
- Request changes freely — revision is normal, not failure.
- If you're rubber-stamping, stop; that's the signal you've stopped adding the human value the method depends on.

### Walking skeleton & the autonomy ladder

The first Construction **Bolt** is the **walking skeleton** — the thinnest end-to-end slice — and it's **always gated and interactive** so you confirm the overall shape before the rest is built. Immediately after you approve it, the **ladder prompt** asks whether the remaining Bolts run **autonomously** or stay **gated**. Choose deliberately: `autonomous` is fast but front-loads your trust onto that skeleton; `gated` keeps a human at every Bolt. Either way, the walking-skeleton gate itself can't be skipped.

### Keeping context healthy

Long sessions fill Claude Code's context window, triggering **compaction** (it summarizes earlier conversation). AI-DLC is built to survive this: state lives in `aidlc-state.md` and artifacts on disk, and a hidden **recovery breadcrumb** (`.aidlc-recovery.md`) lets the next `/aidlc` detect drift. If it warns of a mismatch after compaction, choose **redo current stage** — completed work is safe on disk. The takeaway: **trust the files, not the chat scrollback.** Approving at gates is also a natural moment to let a long session breathe.

## 🎧 See it (6 min)

*Screencast placeholder — [C5: Working a gate the right way, 6 min].* An agent completes a requirements stage; the reviewer opens the artifact, spots a wrong assumption, **requests changes** with specific feedback, re-reviews, then approves — and answers the ladder prompt with a reasoned `gated` choice.

## 🧪 Try it — graded (25 min)

Continue the workshop run from C4. This lab is **assessed on your gate behavior**, not speed.

1. **Reach a real gate.** Advance your run to the first content gate (e.g. Requirements Analysis).
2. **Read first.** Open the produced artifact in the intent's record dir. In one or two sentences, note what it got right and one thing you'd change.
3. **Request changes.** Use **Request Changes** with *specific* feedback (not "make it better"). Confirm the agent revised the right thing.
4. **Approve deliberately.** Only after re-reading, approve — and observe the `HUMAN_TURN` / progress line.
5. **Ladder choice.** When you reach the walking-skeleton ladder prompt, pick `autonomous` or `gated` and write one sentence justifying it for *this* project.
6. **Context check.** Note where the current stage and scope live in `aidlc-state.md`, so you could resume from the file alone.

✅ **Graded pass = you:** read before approving, gave specific revision feedback, and justified your autonomy choice.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Approval gate | Review / sign-off checkpoint |
| Questions file | Requirements Q&A / decision log |
| Request Changes | Send back for rework |
| Accept-as-is | Waive / approve with known caveats |
| Human turn | Recorded reviewer action (audit evidence) |
| Compaction | Context window summarization |
| Never vibe code | "Don't rubber-stamp" / actually review |

</details>

## ✅ Checkpoint

<details>
<summary>1. Name the three interaction modes and what they share.</summary>

Guide Me, Edit File, Chat. All three converge on the same questions file as the canonical record, and you can switch between them mid-stage without losing answers.
</details>

<details>
<summary>2. What does the human-turn requirement prevent?</summary>

It prevents a model on autopilot from fabricating an approval — the engine refuses to approve unless a real HUMAN_TURN was recorded since the last gate.
</details>

<details>
<summary>3. When does "Accept-as-is" become available, and why does it exist?</summary>

After enough revision cycles (warned after the 2nd, offered from the 3rd). It exists so a stubborn stage can't trap you in an endless revision loop.
</details>

<details>
<summary>4. What's special about the walking-skeleton gate and the ladder prompt?</summary>

The walking skeleton (first Bolt) is always gated and interactive. Right after approval, the ladder prompt sets autonomy mode (autonomous vs gated) for the remaining Bolts.
</details>

<details>
<summary>5. Your session compacts mid-stage and warns of a mismatch. What do you do, and why is it safe?</summary>

Choose "redo current stage." It's safe because completed work and state live in aidlc-state.md and artifacts on disk — you trust the files, not the chat history.
</details>

## Key takeaways

- Three interaction modes, **one questions file** as the record; switch freely.
- Gates offer **Approve / Request Changes**, with **Accept-as-is** as an escape hatch — and **require a human turn**, so approval can't be faked.
- The **walking skeleton** is always gated; the **ladder prompt** sets how much you review afterward.
- Survive compaction by **trusting the files.**
- **Never vibe code** — read before you approve. This is the habit the whole method rests on.

**Next:** [C6 — Greenfield vs. brownfield](C6-greenfield-vs-brownfield.md) *(to be authored)* — how the same skills apply to a new app vs. an existing codebase, and picking your lab track.
