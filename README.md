# Team Task Tracker v1.3 Spark Edition

This build uses **Firebase Authentication, Cloud Firestore and GitHub Pages only**. No Cloud Functions, Firebase Storage, or Blaze billing plan is required. Your existing Firebase project configuration is included in `firebase-config.js`.

## Deploy
1. Firebase Console > Firestore Database > Rules: replace rules with `firestore.rules` and click Publish.
2. GitHub repository: replace root `index.html` and `firebase-config.js` with these files; commit changes. Keep GitHub Pages pointed at `main` / root.
3. Hard-refresh the hosted website. Sign in as manager, task owner and collaborator to test.

## How the free-tier workflow works
- **Delete task** performs a *soft deletion*: the task document remains in Firestore with `deletedAt` and an activity event. It disappears from the calendar/task lists but remains readable by its participants to show the deletion alert. No files are uploaded.
- **Request revision** changes the task status to In Progress and writes an activity event with manager notes. Owners and accepted collaborators see the alert.
- **Read notifications**: the activity's `activityReadBy` array stores read state across devices. Only the most recent task activity event is retained. Older events are not an immutable audit log.
- Existing `notifications` collection messages still work. Incoming invitations remain visible as before.

## Important limitations
- This is **not hard deletion**. Retaining a task is necessary to make its deletion event visible without a trusted backend. Storage grows over time; a separate administrator-led cleanup policy would be needed.
- Task activity events are embedded in the task record. A later event can replace the previous one; this is not guaranteed delivery or an immutable audit trail.
- The manager can still see all task records, including deleted ones, through Firestore; the UI hides them.
- The security rules validate who can delete/request revision and constrain fields, but without a trusted server they cannot guarantee all possible business invariants or tamper-proof audit history.
- Manager role changes, automatic new-assignment notifications, and some other advanced notifications are not implemented in this build.
- Firebase Spark free quotas apply. Test on separate accounts before production use.

## Configuration
- **GitHub Pages:** No settings changes, only upload changed files.
- **Firebase Authentication:** No settings changes.
- **Firestore:** Publish the included new rules.
- **Cloud Functions:** Not used; no deployment.
