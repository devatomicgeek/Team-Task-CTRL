# Team Task Tracker v1.4 Spark Edition

## Deployment
1. In Firebase Console > Firestore Database > Rules, publish `firestore.rules`. Keep a backup of your old rules.
2. Upload `index.html` and `firebase-config.js` to the ROOT of your existing GitHub Pages repository and commit.
3. Hard refresh the live site. No GitHub Pages settings, Firebase authorized domain, or Authentication changes are needed.
4. Use separate manager/member test accounts. Test task deletion, notification dismissal, direct/group/task chat, and leave approvals.

## What's new
- Deleted tasks filtered from all calendar views, lists, and dashboard statistics.
- Read notifications hidden immediately and after refresh.
- Text-only direct, group, and task chat; real-time listeners and latest 30 messages per conversation.
- Leave planner: planned leave visible to team; other managers approve or decline; approved leave appears green on calendar. Managers cannot approve their own leave.
- No Cloud Functions, Firebase Storage, or paid Firebase services.

## Limitations and security
- Chat is a first implementation, not a production-hardened messaging service. Group membership cannot be changed after creation. Task-chat membership changes may require additional synchronization.
- Leave requests do not collect medical reasons or other sensitive notes. All authenticated users can see leave dates.
- Chat unread counts are approximate counters; they may become inaccurate with multiple concurrent devices.
- Soft-deleted task records remain in Firestore to support notifications. Task activity history retains only the most recent event.
- Existing manager role promotion/demotion and automatic task assignment alerts remain unfinished.
- Firestore rules are included but **have not been tested against the live project or Emulator Suite**. Test with non-sensitive accounts before production.
- Firebase Spark quotas apply (reads, writes and storage). A large team or active chat can exhaust free quotas.
- Firebase configuration values are public browser app settings, not Admin SDK credentials.
