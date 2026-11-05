# Team Task Tracker v1.0

## What works now
- Responsive calendar (month/week/day), task cards, task creation and status updates
- Manager and member preview accounts, role promotion/demotion in **demo only**
- Collaboration requests (accept/decline), notifications, manager approval/revision flow
- No attachments or Firebase Storage

## Preview mode
Serve this folder with a local web server, for example `python3 -m http.server 8000`, and open `http://localhost:8000`. The UI starts with sample data. The preview is in-memory and resets on refresh. Switching the preview account lets you test member/manager flows.

## Firebase integration
1. Create a Firebase project and a web app.
2. Enable Firebase Authentication > Email/Password and create users in the Firebase Console.
3. Enable Cloud Firestore.
4. Paste your web app configuration into `firebase-config.js`.
5. Provision a `users/{firebaseAuthUid}` document for each user with fields `id`, `name`, and `role` (`manager` or `member`). Do this from a trusted admin environment. Do not allow public users to set their own role.
6. Deploy **reviewed security rules** before enabling real users. The included `firestore.rules` is a restrictive baseline. It does not provide a secure client-side promotion/demotion endpoint.
7. Host the files via GitHub Pages and add your Pages domain under Firebase Authentication > Settings > Authorized domains.

## Important security and feature limits
- Live Firebase sync uses Firestore listeners for `users`, `tasks`, `requests`, and `notifications`. This v1 prototype uses full-collection listeners, so it is appropriate only for small controlled testing. Optimize per-user queries, pagination and indexes before larger deployments.
- **Live manager promotion/demotion is deliberately disabled**. Use a trusted backend (Cloud Functions + Admin SDK) to validate the actor and last-manager safeguard, then change roles atomically. Do not implement this as an unrestricted client-side write.
- The included Firestore rules restrict manager role changes to a trusted backend, but additional authorization review and rule testing are necessary before production.
- Firestore listener delivery, notifications and collaboration writes are not atomic; production should use transactions/Cloud Functions to enforce acceptance and notifications consistently.
- This version has in-app notifications only, not browser push notifications.
- Task status edits are basic; approval state transitions need stronger server-side enforcement before production.
- In Firebase mode, new users must be provisioned by an administrator. No self-registration is exposed.
- For local preview use a web server; `file://` will not reliably load ES modules.

## GitHub Pages and Firebase changes
- GitHub Pages: upload `index.html` and `firebase-config.js` to the published repository root; configure Pages once if not already enabled. Later code-only updates normally do not require Pages reconfiguration.
- Firebase: create/configure Authentication, Firestore, security rules, authorized domains, and user documents. Cloud Functions are required for secure live role management and robust notification workflows.
