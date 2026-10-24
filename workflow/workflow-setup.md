# Workflow Setup

**Tool:** Freshservice → Admin → Workflow Automator → Tickets → Event Based Workflow
**Name:** VIP Ticket → Slack #it-internal

```
[Ticket is raised] → [VIP and not onboarding/offboarding?] —YES→ [Post to Slack]
                                     └—NO→ (do nothing)
```

## Block 1: Event (green)

| Setting | Value |
|---|---|
| Performed by | Anyone |
| Event | Ticket is **raised** |

Why "raised": it fires once, when the ticket is created. Not on every reply.

## Block 2: Condition (orange)

| Setting | Value |
|---|---|
| Match | **all** |
| Check 1 | Requester Fields → VIP User → **Selected** |
| Check 2 | Ticket Fields → Source → **does not include** → Journey, Employee Onboarding, Employee Offboarding |

Why check 2: onboarding/offboarding tickets are created automatically in an HR VIP's name. They all have the Source "Journey."

Why "all": a ticket must pass **both** checks. "any" would let almost everything through.

## Block 3: Action (blue)

| Setting | Value |
|---|---|
| Action | Trigger Webhook |
| Request Type | POST |
| Callback URL | Slack incoming webhook URL (**secret, never commit**) |
| Encoding | JSON |
| Content | **Advanced** (not Simple) |
| Body | See `slack-message.json` |

Why Advanced: Slack requires a field named `text`. "Simple" sends Freshservice's own field names, and Slack rejects them with `no_text`.

## Slack App

| Setting | Value |
|---|---|
| Created at | api.slack.com/apps |
| Scopes | `incoming-webhook` only |
| Feature | Incoming Webhooks → one webhook for the IT channel |
| Install | Requires Slack admin approval |
