# ring-scanner-android

Android app paired with a custom ring-shaped scanner device. The device firmware
(written in C++) reads QR codes; this app connects to it over Bluetooth and uses
the scans to drive tasks and workflows.

Built in 2019 and open-sourced once the surrounding product stack changed.

## How it fits together

```
ring device (C++ firmware) --Bluetooth serial--> this app --> workflow backend
```

`app/src/main/java/kratos/ringscannerapp/CommunicationsTask.java` holds the
Bluetooth socket handling: it opens an SPP connection to the device and reads the
scan payloads.

## Stack

- Java, Android (Gradle build)
- Bluetooth serial profile (SPP UUID `00001101-...`) to the device
- QR-code scan payloads as the input

## Build

```
./gradlew assembleDebug
```

`local.properties` with your SDK path is required and is not committed.

## Notes

- Scan-to-workflow mapping lived on the backend, so the app stays thin.
- Only the app is here; the device firmware is not part of this repo.
