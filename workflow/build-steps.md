# Build It From Scratch

About 45 minutes. You need: Slack app-builder access (admin approval), Freshservice admin (Requesters + Workflow Automator).

## Part 1: Slack (the mail slot)

1. Go to **api.slack.com/apps** → **Create an App** → **Blank app**. Name it, pick your workspace.
2. Add one permission: **incoming-webhook**. Skip Events. Click **Create**.
3. Left menu → **Incoming Webhooks** → turn **On** → **Request to Add New Webhook**. Ask an admin to approve.
4. After approval → **Add New Webhook** → pick the IT channel → **Allow**.
5. *(Optional)* **Basic Information** → **Add App Icon** (square, 512 to 2000 px).

> 🔒 Copy the URL only with Slack's **Copy** button, straight into Freshservice. Never paste it anywhere else.

## Part 2: Freshservice (who is a VIP)

6. **Admin → Requesters** → open a person → **Edit** → tick **Mark as VIP** → **Update**.
7. Check the list: **Requesters → VIP** tab.

> ⚠️ If nobody is marked VIP, the alert never fires and nothing warns you.

## Part 3: Freshservice (the robot's brain)

8. **Admin → Workflow Automator → Create → Workflow** → Tickets → Event Based.
9. **Event:** Ticket is **raised**, by **Anyone** → Save.
10. **Condition:** drag onto the arrow. Match **all**. Add both checks (see `workflow-setup.md`) → Save.
11. **Action:** drag onto the **YES** arrow → Trigger Webhook → POST → paste URL → JSON → **Advanced** → paste `slack-message.json`.
12. Fill in sample values → **Test Webhook** → must say *successful* and post in Slack → Save.
13. **Activate** → **Confirm** → reload → must say **Active**.

## Part 4: Prove it works

14. Test VIP submits a ticket → alert posts.
15. Non-VIP submits a ticket → nothing posts.
16. Next real onboarding → no VIP alert. Check **View execution logs**.
17. Close test tickets. Un-VIP the test account.

## Changing it later

Open workflow → **Edit as Draft** → change → Save → **Activate → Confirm**.
The live version keeps running while you edit. The workflow gets a **new ID** after each publish.
