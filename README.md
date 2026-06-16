# Alex Offline Assistant

Alex Offline Assistant is a personal Android voice assistant named **Alex**. It is designed for private device use, offline command execution, and transparent foreground operation.

## What Alex Does

- Listens for the wake word: `Alex`
- Runs as a visible foreground service with the notification `Alex is listening locally`
- Parses commands with a local rule-based command registry
- Uses Android TextToSpeech for spoken feedback
- Supports lock phone, alarms, timers, app launch, confirmed calls, message drafts, volume, flashlight, settings screens, and safe accessibility navigation
- Stores settings, trusted contacts, and command history locally
- Supports Device Admin for locking the phone when personally granted

## What Alex Does Not Do

- No voice unlock
- No lock-screen PIN/password/pattern/biometric storage
- No Android keyguard bypass
- No password injection
- No hidden launcher behavior
- No hidden foreground service notification
- No silent surveillance
- No raw audio storage
- No Firebase, analytics, cloud backend, remote assistant API, or hosted language service
- No internet permission

## Offline Processing

Alex is offline and rule-based. Speech recognition is intended to use a bundled or manually installed Vosk model. Natural language handling is local command matching, aliases, fuzzy matching, and slot extraction. The app does not send audio, text, logs, contacts, or device data anywhere.

## Offline Voice Model Setup

Place an unpacked Vosk English or Indian English small model in:

```text
app/src/main/assets/vosk-model-small-en-us-0.15/
```

The folder currently contains a placeholder README. Alex never downloads a model at runtime.

## Permission Setup

The setup screen shows status for:

- Microphone
- Notifications
- Device Admin
- Accessibility Service
- Contacts
- Phone
- Exact alarm access
- Battery optimization exclusion

Grant only the permissions you need. Direct calling requires `CALL_PHONE`; otherwise Alex opens the dialer.

## Device Admin Setup

Enable Device Admin from the setup screen. This allows `lock phone` via `DevicePolicyManager.lockNow()`. Alex uses Device Admin only for declared policy actions and never stores the device credential.

## Accessibility Setup

Enable `Alex Assistant Navigation` in Android Accessibility settings. Alex uses it only for visible navigation actions such as Back, Home, Recents, notifications, quick settings, and power menu. It blocks password, banking, payment, and security-like automation.

## Locked Mode

Allowed by default while locked:

- Wake word detection
- Time, date, battery
- Set alarm
- Set timer
- Stop alarm/timer
- Trusted-contact calls with confirmation
- Lock phone
- Volume
- Flashlight
- Open power menu
- Limited assistant status

Blocked while locked:

- Voice unlock
- Unknown calls
- Untrusted contacts
- Private messages
- Photos/files
- Banking/payment apps
- Typing/dictation
- Security settings
- Password entry
- Payment approval

## Supported Commands

See [COMMANDS.md](COMMANDS.md).

## Developer

Alex is maintained by Suraj.

- Website: https://mrsuraj.rf.gd
- GitHub: https://github.com/5ur4jd-dev

## Known Android/OEM Limitations

- Background microphone behavior varies by Android version and OEM power policy.
- Exact alarms may require user approval on Android 12+.
- Restart/reboot is not available to normal Device Admin apps; use the power menu command instead.
- Power off is not exposed as a normal third-party API; Alex can open the power menu through Accessibility where supported.
- Some Clock, Phone, SMS, and OEM Settings apps may force UI confirmation.

## Troubleshooting

- **Offline voice model is missing:** place the Vosk model under `assets/vosk-model-small-en-us-0.15`.
- **Listening stops in background:** exclude Alex from battery optimization.
- **Lock phone does not work:** enable Device Admin.
- **Restart does not work:** Android does not expose reboot to normal Device Admin apps. Enable Accessibility and use `open power menu`.
- **Navigation commands do not work:** enable Alex Accessibility Service.
- **Calls open dialer instead of calling:** enable direct calling and grant Phone permission.
- **No command history:** history starts after commands are recognized; raw audio is never logged.
