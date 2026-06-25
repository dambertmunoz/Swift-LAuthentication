# LocalAuthentication Swift Wrapper

iOS framework and demo app that wrap Apple's `LocalAuthentication` APIs behind a small reusable interface.

The project demonstrates biometric authentication flows for Face ID, Touch ID, passcode fallback, success handling, rejection, and unavailable-biometry states.

## What This Project Shows

- `LAuthentication` framework target.
- `LAuthentication.shared.evaluatePolicy` wrapper method.
- Demo UIKit app under `DemoLA`.
- Separation between authentication API access and screen-level alert handling.

## Usage

```swift
LAuthentication.shared.evaluatePolicy(reason: "Authenticate to continue") { success in
    if success {
        // Unlock protected flow.
    } else {
        // Authentication failed.
    }
} rejected: { error in
    // Biometry unavailable, not enrolled, locked out, or cancelled.
}
```

## Running

```sh
open LAuthentication.xcodeproj
```

Run the demo app on a physical device for full biometric coverage. Simulator behavior is limited.

## Technical Notes

- Always provide a user-facing authentication reason.
- Handle unavailable biometry separately from failed authentication.
- Do not treat biometric success as authorization by itself; pair it with the app's real session/security model.
- Prefer dependency injection around this wrapper when testing protected flows.
