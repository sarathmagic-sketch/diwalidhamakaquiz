# Diwali Dhamaka — Live Quiz App

Node.js + Socket.IO quiz app for 50–100 players.

## Pages
- `/` Host/projector screen: QR code, countdown, answer percentages and leaderboard.
- `/play` Participant phone screen.
- `/admin` PIN-protected host controls and editable question bank.

## Run locally
Requires Node.js 18+.
```bash
npm install
ADMIN_PIN=your-private-pin npm start
```
Open http://localhost:3000. For phones on the same Wi-Fi, use the host computer's LAN IP and port 3000. For internet QR joining, deploy to a public HTTPS host.

## Deploy to Render
1. Put this project in a GitHub repository.
2. Create a Render Web Service from the repository.
3. Build command: `npm install`; start command: `npm start`.
4. Set environment variable `ADMIN_PIN` to a private PIN.
5. Deploy, open `/admin` to edit questions and `/` on the projector.
6. QR is generated automatically using the deployed host URL.

## Host flow
1. `/admin` -> enter host PIN. Default local PIN is `2468`; change it before public deployment.
2. Review/edit/remove/add questions and save.
3. Set 30 seconds and break after 25.
4. Project `/`; players scan QR and enter names.
5. Start/restart from admin. After each timeout, the host screen shows answer percentages and leaderboard.
6. Press Next/Continue after results. After Q25, the game pauses for a break. Press Next/Continue to start Q26, or end the event there.
7. After Q50, the final leaderboard remains visible.

## Notes
The server enforces the deadline and rejects late answers. Live game state is held in memory, so use one server instance for the event. The question bank is stored in `data/questions.json`; on hosts with ephemeral filesystems, edits may reset after restart/redeploy. Use persistent storage or a database for long-term use. Do not scale to multiple instances without shared state.
