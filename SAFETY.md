# Safety Model

Alex is built around explicit safety boundaries:

- No voice unlock
- No lock-screen credential storage
- No password typing
- No Android keyguard bypass
- No root, exploit, private, or hidden APIs
- No internet permission
- No silent recording
- No hidden foreground service
- No raw audio logs

## Command Sensitivity

- `LOW`: time, battery, volume, flashlight, timer
- `MEDIUM`: open app, open settings, draft message, set alarm
- `HIGH`: call contact, reboot, power menu, tap confirm
- `BLOCKED`: unlock phone, password input, factory reset by voice, wipe data by voice, send money, payment approval, silent spying

## Confirmations

Sensitive actions require spoken confirmation within 10 seconds. Examples:

- `call Mom` -> `confirm call Mom`
- `restart phone` -> `confirm restart`

## Accessibility

Accessibility is limited to visible UI actions. Alex does not harvest screen text into logs and blocks automation on password, payment, banking, and security-like screens.

## Locked Mode

Locked mode allows only small, explicit tasks. Unknown calls, private data, app typing, files/photos, banking/payment apps, and security changes require unlock.
