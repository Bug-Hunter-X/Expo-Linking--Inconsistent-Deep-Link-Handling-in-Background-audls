# Expo Linking: Inconsistent Deep Link Handling in Background

This repository demonstrates a bug in the Expo `Linking` API where deep link events are not consistently handled when the app is in the background on Android.  The `Linking.addEventListener` method, while working correctly in the foreground, may fail to trigger when the app is backgrounded.

## Bug Description

The issue lies in the unreliability of receiving deep link events when the app is already running but minimized. This makes it difficult to handle user interactions initiated via deep links when the app is not actively in use.

## Solution

The proposed solution involves a combination of strategies to ensure consistent deep link handling regardless of the app's state:

1. **Using `Linking.getInitialURL()`:**  This method retrieves any initial URL from the last app launch, helping catch events missed by the event listener.
2. **Implementing a background service (Android):** Although this adds complexity, for complete reliability, a background service maintains active listening for deep links even when the main app is not active.  Note that background restrictions vary between Android versions, and require configuration.
3. **Improved Error Handling:**  The revised code includes better error handling to gracefully manage situations where deep link events are not received.

## Reproduction Steps

1. Clone this repository.
2. Run the app on an Android device.
3. Minimize the app.
4. Open a deep link (e.g., using a web browser).
5. Observe whether the deep link is correctly handled.

## Additional Notes

This bug report aims to document the issue and provide a robust solution. The behavior may vary slightly depending on the Android device and Expo SDK version.  Consider testing on different devices and versions for comprehensive validation.