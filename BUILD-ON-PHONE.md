# Build the J.A.R.V.I.S. APK from your phone

This project includes a GitHub Actions workflow that builds a debug APK in the cloud. This means you do not need to install Android Studio on your phone.

## Steps

1. Download and extract `JARVIS-Android-Starter-v5.zip` on your phone or computer.
2. Sign in to GitHub and create a **new empty repository** named `jarvis-android` (do not add a README or license because the project already has files).
3. Upload the **contents** of the extracted `JARVIS-Android-Starter-v4` folder into the repository. Make sure `.github/workflows/build-apk.yml` is included. On GitHub mobile web, you may need to use your browser's desktop-site option; uploading a folder may require selecting files individually or using GitHub's supported upload flow.
4. Open the repository's **Actions** tab and enable workflows if GitHub asks.
5. Select **Build JARVIS Android APK**, tap **Run workflow**, then run it on the `main` branch. A push to `main` also triggers a build.
6. Wait for the workflow to finish successfully. Open that workflow run and find **Artifacts** near the bottom.
7. Download `jarvis-debug-apk`, extract it, and install `app-debug.apk` on your OPPO phone. Android may ask you to allow installation from the browser or file manager you used. Only enable that permission for the app you trust, then turn it off again afterward if desired.

## Important

- The source has not been compiled or tested on the target phone in this environment. A cloud build is the next verification step; if it fails, open the workflow log and fix the reported error before installing.
- This is a debug APK, not a Play Store release.
- The AI backend is optional. Broader AI responses require deploying the included backend and configuring its URL in app settings. Keep the API key on the server, never in the Android app.
- The app does not have always-on wake-word listening or unrestricted access to every phone app. Android permissions and user confirmation remain required for many actions.
