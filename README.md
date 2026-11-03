# Jane Paper

Small offline Android drawing-board prototype, version 0.2.

## Features

- White canvas and a bottom-right Tools selector.
- Pen, eraser, four colors, undo and clear confirmation.
- One current drawing saved in app-private storage and reopened on launch.
- Deliberate PNG export using Android's system file picker. Choose a local folder to keep exports on the device.
- No Android permissions requested, including no Internet permission. No account, backend or live assistant connection.

## Source

`src/paper/jane/offline/MainActivity.java` contains the native Android activity and canvas. `AndroidManifest.xml` declares the application. This repository intentionally contains source and this README only; no APKs, signing material, credentials, drawings or device logs.

## Building

Use an installed Android SDK and JDK. The prototype was compiled with JDK 17, Android SDK platform 37 and build-tools 36, targeting API 34 with minimum API 23. Compile the Java source against android.jar, convert classes with D8, package the manifest with aapt, add classes.dex, zipalign and sign using your own locally managed key. No Gradle wrapper, signing configuration or automated deployment is included. Updating an existing installation requires its original signing key; otherwise Android will reject the update. Do not uninstall an existing copy merely to change keys, because that removes app-private drawings.

## Touch update

Version 0.2 moves JSON serialization and disk flushing to a single background executor, caches completed strokes instead of rebuilding all paths every frame, handles active-pointer lifts and cancellation, and renders isolated taps as dots. Historical touch samples remain included. On first load, the existing saved drawing is copied to an app-private pre-update JSON backup before reading it.

## Verification and limits

The prototype was installed on an Android tablet. Simulated touchscreen gestures verified strokes, color, erasing, undo, local persistence, offline cold reopen and local PNG export. Version 0.2 preserved an existing drawing and passed line, dot and undo checks. These checks do not establish physical finger/stylus responsiveness: a user reported poor hand-input registration in version 0.1; real finger testing of the update is still pending. Multi-touch handling was reviewed but not independently exercised with a physical multi-touch test.

This is an early prototype, not a production note archive. It keeps one current editable drawing, not a notebook. Clear replaces the saved current drawing after confirmation. Export important work regularly. Rotation during export and long-running performance have not been validated. Saves run asynchronously; abrupt process termination or power loss before completion can lose the latest unsaved change. The app has no continuous connection to an assistant.
