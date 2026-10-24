# Changelog

## 2026-10-14: Fix #1, stop onboarding/offboarding alerts
- **Problem:** HR VIPs start onboardings. Freshservice auto-creates tickets in their name, which triggered VIP alerts.
- **Fix:** Added Condition check `Source does not include Journey / Employee Onboarding / Employee Offboarding`. Set Match to **all**.
- **Result:** Past 30 days: 30 alerts → 7 (all real requests). No VIPs removed.

## 2026-10-13: Initial build
- Created Slack app with `incoming-webhook` scope only. Admin approved.
- Added webhook for the IT channel. Added app icon.
- Flagged executives and HR as VIPs in Freshservice.
- Built Workflow Automator rule: Ticket raised → VIP? → Trigger Webhook.
- Test Webhook passed. Activated.
