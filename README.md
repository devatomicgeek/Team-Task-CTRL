# Team Task Tracker v1.6 Spark Edition

## Changes
- Sidebar: removed top logo, brand name, and version badge; profile now starts the sidebar. Brand and version moved to the sidebar footer.
- New Arcade navigation: retro Pong practice vs computer, plus 1v1 teammate challenges, accept/decline, and WebRTC DataChannel gameplay.
- Existing v1.5 calendar, chat, leave planner, and task workflows retained.

## Deploy
1. Back up your current GitHub files and Firestore rules.
2. Upload **index.html**, **arcade.js**, and **firebase-config.js** together to the same GitHub Pages directory. Keep your existing Firebase config values if the packaged config has placeholders.
3. In Firebase Console > Firestore Database > Rules, replace with **firestore.rules** and publish. This is **required** for multiplayer Pong.
4. Wait for GitHub Pages deployment and hard-refresh both players' browsers. No GitHub Pages settings, Auth domains, Cloud Functions, or billing changes should be needed.
5. Test with two separate authenticated accounts. Challenge, accept, then join the match. Practice mode also works without Firebase.

## Limitations / safety
- **WebRTC uses a public STUN server only**. Some office networks, mobile carriers, or NAT configurations need a TURN relay. No TURN service is bundled, and reliable connectivity on all networks is not guaranteed on Spark-only resources.
- Firestore handles only matchmaking and WebRTC SDP/ICE signaling. Live paddle and ball state use peer-to-peer DataChannels. Firebase free quotas still apply to signaling.
- Games are casual, not cheat-proof. The host simulates physics; final scores are not independently verified. No public leaderboard in this release.
- Match records and ICE candidates are retained; an administrator should establish a retention/cleanup policy. Spark has no automatic Cloud Functions cleanup.
- No Firebase emulator or real two-device connectivity test was performed here. Verify Firestore rules and gameplay with real accounts before general rollout.
- Existing v1.5 caveats around task-chat membership and role management remain.
