# J.A.R.V.I.S. Android Starter

A native Android starter for a personal assistant, not just a web dashboard. It currently includes:

- Native Android app shell with a cinematic dark/cyan HUD and animated, reactor-inspired interface.
- Android speech recognition through the device speech service (manual mic activation).
- Android Text-to-Speech output.
- Local commands for date/time, battery level, notes, tasks, timers, web search, and opening supported Android screens/apps.
- Speech playback can be interrupted with “stop speaking”.
- Local persistence for notes, tasks, personality choice, and backend URL.
- Five response-style profiles with distinct J.A.R.V.I.S., F.R.I.D.A.Y., M.A.Y.A., engineering, and discreet-assistant behavior.
- More composed spoken delivery, attempting a UK English TTS locale when the phone has a compatible voice installed. This is device TTS, not the original film voice.
- Optional secure AI backend endpoint.
- GitHub Actions workflow to build a debug APK.

## Honest limitations

This is an improved starter build, not a complete movie-level assistant. The cinematic interface and response style are inspired by the fictional assistant concept; they do not reproduce the film system or its original voice. Background always-on wake-word detection is **not implemented**. Reliable wake-word detection and deep phone control require additional native Android engineering, careful permission handling, and battery testing. Speech recognition may use Google's or another installed speech service and may require internet depending on device configuration. Offline TTS depends on voices installed on the phone. Local commands work without an AI backend; open-ended AI needs a configured backend and provider key.

## Build an APK using GitHub Actions from your phone

1. Create a GitHub repository and upload the contents of this folder.
2. Ensure the default branch is named `main`.
3. Open the repository's **Actions** tab.
4. Select **Build JARVIS Android APK** and press **Run workflow**.
5. When the workflow finishes, open its run page and download the `jarvis-debug-apk` artifact.
6. Extract the downloaded artifact ZIP and install `app-debug.apk` on your Android phone. Android may ask you to allow installation from that source. Only install APKs you built or trust.

You can also open this project in Android Studio and run the `app` configuration on a device.

## Optional AI backend

The app calls a backend URL ending in `/chat`. The included backend uses the Gemini API with the key kept on the server.

1. Install Node.js 20+ on a server or computer you control.
2. In `backend`, run `npm install`.
3. Copy `.env.example` to `.env` and set `GEMINI_API_KEY` and optionally `PORT`.
4. Run `npm start`.
5. Host it behind HTTPS. Do not expose a backend with no authentication to the public internet; add authentication/rate limiting before public deployment.
6. Enter the HTTPS `/chat` endpoint in the app's Settings.

A Gemini key may have usage limits or costs according to the provider's current terms. Do not put the key in Android source code. Set `GEMINI_MODEL` if the provider model name changes. The included backend has a basic per-process rate limit, but that is not a substitute for authentication and a production-grade shared rate limiter; do not expose it publicly without additional protection.

## Supported local commands

- `who are you?`
- `system status` or `run diagnostics`
- `what can you do?`
- `what time is it?`
- `what is today's date?`
- `remember buy a notebook`
- `show notes`
- `create task revise vectors`
- `show tasks`
- `open YouTube`
- `open Chrome`
- `open dialer`
- `open camera`
- `open settings`
- `open maps`
- `search for Newton's laws`
- `what is my battery level`
- `start a 25-minute timer`
- `cancel timer`
- `stop speaking`
- `calculate (12 + 8) / 4`
- `what is Newton's second law?`
- `what is the quadratic formula?`
- `what is the speed formula?`
- `help`

## Current implementation notes

- The timer uses an in-process coroutine. Keep JARVIS running; Android may stop the process or delay work in the background. It is not a guaranteed alarm-clock replacement.
- Basic arithmetic is evaluated locally with a restricted arithmetic parser; it does not execute code.
- A few basic offline educational replies are included (Newton's second law, quadratic formula, and speed formula). They are starting points, not a replacement for a configured AI tutor.
- Speech input launches the device's speech-recognition service. It is a tap-to-speak flow, not an always-listening wake word.
- `open camera` launches a compatible camera capture activity; it does not silently take a photo.
- `open dialer` opens the dialer only. It does not place a call.
- `search for ...` opens a browser search. It is not a built-in web-search API.
- Battery information is read from Android's sticky battery broadcast where available.

## Next native development milestones

- Add an actual local wake-word engine with explicit opt-in and an Android foreground service where permitted.
- Improve runtime permission guidance and add a native wake-word engine with explicit opt-in where feasible.
- Add task completion/editing, reliable background timer notifications, and calendar integration.
- Add authentication and rate limits to the AI backend before public deployment.
- Add native intent handlers only for user-approved actions and test each action on the target OPPO device.


## Mind Network (v4)

The Android client now includes a role-based multi-specialist routing layer inspired by the attached Eonverse-style video:
- **NEXUS** — central coordinator
- **AGORA** — revenue, business opportunities and value
- **CODEX** — knowledge, research and learning
- **FORGE** — building, coding and delivery
- **TRESOR** — finance education, budgets and costs
- **HERALD** — growth, content and campaigns
- **SHIELD** — security, privacy and reliability

The client includes 29 selectable specialist roles. In **AUTO** mode, requests are routed by simple keyword heuristics; users can instead pin a universe or one specialist role. The selected route is sent to the configured backend, which adds the role to the system instruction. This is a **single AI model with role prompts and routing**, not 29 independent AI models or autonomous agents. The video does not provide enough technical detail to reproduce the creator's underlying system exactly, so this implementation uses the visible domain concepts and clearly labeled role-based inference.

The new routing UI and backend have not been compiled or device-tested in this environment. The existing APK limitations still apply.

## Full collection index (v5 source package)

See [`ai-universe-collection.json`](ai-universe-collection.json) for a structured catalogue of every main universe and its subtypes, plus the five personality modes. The in-app collection dialog displays the grouped hierarchy; universe and specialist chips let you select the route. This is a practical role-based collection, not a claim that all characters shown in the video are separate running models.

For phone-based cloud compilation steps, see [`BUILD-ON-PHONE.md`](BUILD-ON-PHONE.md). The APK still needs to be built by the included GitHub Actions workflow and verified before installation.
