# Team Task Tracker v1.2

## Deployment
1. Replace `index.html`, `firebase-config.js`, and other project files in your existing GitHub Pages repository root. No GitHub Pages reconfiguration is needed.
2. In Firebase Console > Firestore Database > Rules, replace existing rules with the bundled `firestore.rules` and click **Publish**. This is **required** for v1.2 collaboration acceptance.
3. Keep the same Firebase project, Authentication users, and authorized domain. No new Firebase collections or domain configuration required.
4. Test with two different Firebase accounts. Send an invitation, accept it, confirm the task appears for recipient, then send a separate invitation and decline it.

## Changes
- Collaboration acceptance is a single atomic Firestore transaction. Security rules validate a pending invitation and restrict collaborator changes to exactly the accepting recipient.
- Decline only updates invitation status.
- Status edits write only the status field.
- Notification read changes write only the read field.
- Improved invitation error reporting.

## Known limitations
- This is still a testing build, not production ready.
- No backend-generated assignment/approval/response notifications; incoming invitations appear as notification-center items.
- Role promotions/demotions still need trusted server-side implementation.
- The recipient may see 'Task unavailable' before accepting because task reads are restricted.
- Existing managers' non-status task editing is not yet implemented.
- The Firebase rules use `getAfter()` to enforce cross-document consistency; validate in Firebase Rules Playground/emulator before team rollout.
