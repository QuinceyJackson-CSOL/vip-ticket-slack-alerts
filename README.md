# VIP Ticket Alerts → Slack

**When an important person asks IT for help, IT finds out in seconds.**


---

## The Problem

Imagine a school help desk. Hundreds of requests come in: "I forgot my password," "My mouse is broken."

Now the **principal** sends one: *"The projector died and the assembly starts in 5 minutes!"*

That request lands in the same pile as everything else. By the time someone notices, it's too late.

## The Solution

We built a robot that watches the pile.

When a request comes from a **VIP** (a very important person), the robot instantly sends a message to the IT team's group chat. Nobody has to keep checking. The important stuff comes to them.

```
VIP asks for help  →  Robot checks "Is this a VIP?"  →  YES  →  Message pops up in the IT chat
```

What the IT team sees:

> 🚨 **VIP ticket #902** from Jane Exec
> > Zoom not working, board call in 8 minutes
> Open in Freshservice

---

## How It Works (3 Pieces)

| Piece | What it is | Like... |
|---|---|---|
| **Freshservice** | Where help requests (tickets) are stored | The help desk inbox |
| **Workflow Automator** | A rule: *"When THIS happens, do THAT"* | The robot's brain |
| **Slack Webhook** | A private address that posts into one chat channel | A mail slot into the group chat |

### The robot's brain has 3 blocks

1. **Event (the trigger):** A new ticket is created.
2. **Condition (the question):** Is the person a VIP? **AND** is this a real request (not an automatic onboarding ticket)?
3. **Action (the job):** Send a message to the Slack mail slot.

If the answer is **NO**, the robot does nothing.

---

## Key Words

| Word | Simple meaning |
|---|---|
| **Automation** | A rule that does a job for you, every time, without you |
| **Webhook** | One app "ringing the doorbell" of another app when something happens |
| **Trigger** | The thing that starts the automation |
| **Condition** | A yes/no question the automation asks |
| **Action** | What the automation actually does |
| **JSON** | A simple text format apps use to talk: `{"text": "hello"}` |
| **Placeholder** | A fill-in-the-blank like `{{ticket.subject}}` that gets swapped for real info |

---

## A Bug We Found (and Fixed)

**What went wrong:** HR staff are VIPs. When HR hires someone, the system *automatically* creates setup tickets in their name. The robot thought those were VIP emergencies and sent alerts for every new hire.

**The wrong fix:** Remove HR from the VIP list. (They'd lose alerts for their *real* problems.)

**The right fix:** Teach the robot one more question: *"Was this ticket made automatically by onboarding?"* If yes, skip it.

**Result:** In one month, alerts dropped from **30 → 7**. All 7 were real requests.

> **Lesson:** A robot does exactly what you tell it, not what you meant. When it makes a mistake, don't remove people. Find what makes the bad cases different, and add a rule for it.

### One tricky setting: "Match any" vs. "Match all"

When the robot asks two questions:

- **Match all** = BOTH must be true (VIP **and** not onboarding) ✅
- **Match any** = just ONE must be true (VIP **or** not onboarding) ❌ That's almost every ticket, and the chat floods.

---

## How We Tested It

1. **Test button:** Sent a fake message to make sure Slack accepts it. ✅
2. **VIP test:** A test VIP account submits a ticket. Alert should appear. ✅
3. **Non-VIP test:** A regular person submits a ticket. No alert. ✅
4. **Onboarding test:** HR starts a new hire. No VIP alert. ✅

---

## Safety Rules

- 🔒 **The webhook URL is a secret.** Anyone who has it can post in the chat. It is **never** saved in this repo.
- 🔑 **The Slack app has one permission only:** post to one channel. It can't read messages or see users.
- ✋ **Admins approve new apps.** That's on purpose.

---

## What's in This Repo

| File | What it is |
|---|---|
| `README.md` | This page |
| `workflow/workflow-setup.md` | Exact settings for each block |
| `workflow/slack-message.json` | The message template sent to Slack |
| `workflow/build-steps.md` | Step-by-step guide to rebuild it from scratch |
| `CHANGELOG.md` | Every change, when, and why |

---

## Skills This Project Shows

- Connecting two apps with a **webhook**
- Building **if/then automation** logic
- Formatting data as **JSON**
- **Debugging** a real problem using data, not guesses
- **Least-privilege security** (only the access you need)
- **Documenting** so someone new can maintain it

---

Built by **Quincey Jackson**, IT, October 2026.
