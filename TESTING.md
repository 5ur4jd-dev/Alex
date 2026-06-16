# Testing

## Unit Tests

Run:

```bash
./gradlew test
```

Covered areas:

- Command parsing
- Fuzzy aliases
- Time parsing
- Timer duration parsing
- Contact matching
- Locked mode policy
- Confirmation flow
- Command registry safety entries

## Manual Checklist

- Wake word Alex works offline
- Command mode activates after wake word
- Lock phone works with Device Admin
- Restart command reports unsupported and suggests the power menu path
- Power menu opens through Accessibility if enabled
- Call trusted contact works with confirmation
- Unknown call is blocked while locked
- Alarm sets while locked
- Timer rings over lock screen
- Stop timer by voice
- Open app works while unlocked
- Sensitive app is blocked while locked
- Message draft queues while locked
- Message draft opens after unlock
- No internet permission present
- App does not store raw audio
- Foreground notification always visible while listening

## Security Review Notes

- Verify `AndroidManifest.xml` has no `android.permission.INTERNET`.
- Verify Device Admin XML only declares policies actually used.
- Verify Accessibility service description is clear.
- Verify logs contain command metadata only, not raw audio.
