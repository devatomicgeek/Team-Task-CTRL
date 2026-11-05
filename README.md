# Team Task Tracker v1.5 Spark Edition

## Changes from v1.4
- Edge-to-edge full-browser layout: removes fake window border, rounded outer shell, outer margins and width cap. Responsive mobile layout retained.
- Chat list permission fix: participant-scoped queries match participant-based Firestore rules. Task authorization is checked when task chats are created and when sending messages, rather than as an extra condition on chat collection queries.
- Chat send uses a Firestore transaction to update message count and the sender read counter together. Solo-owner task chat creation now supported.
- Chat entries for known soft-deleted tasks are hidden from active conversation list.

## Deployment (IMPORTANT)
1. Back up your current Firestore rules. Publish the **entire** included `firestore.rules` in Firebase Console > Firestore Database > Rules. **This is required** for the chat fix.
2. Replace `index.html` and `firebase-config.js` in the root of your existing GitHub Pages repository, then commit. Keep your existing Firebase project config; the included config is copied from v1.4.
3. Hard-refresh the site after GitHub Pages deploys. **No GitHub Pages settings, Firebase Auth authorized domains, or billing changes are expected.**
4. Test using two separate accounts: direct chat, group chat, task chat, read counters, manager/member task visibility, deletion, and leave approval.

## Security and known limitations
- **Not validated against a live Firebase project or Firestore emulator.** Back up rules and test with non-sensitive accounts first.
- Participant membership on task chats is fixed at creation. Changes to task collaborators do not yet revoke existing chat membership. **Do not use task chats for sensitive material until membership synchronization is implemented.**
- Chat members may read old messages even if the task was soft-deleted; sending new task messages is blocked. Group membership management is not yet available.
- Firestore read counters can still be affected by multiple concurrent devices; test before wider rollout.
- No Cloud Functions, Storage, or paid services. Firebase Spark usage quotas still apply.
- Manager role changes and automatic task-assignment notifications remain unfinished.
