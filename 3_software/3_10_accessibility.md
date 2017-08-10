## 3.10\. Accessibility

Android provides an accessibility layer that helps users with disabilities to
navigate their devices more easily. In addition, Android provides platform APIs
that enable accessibility service implementations to receive callbacks for user
and system events and generate alternate feedback mechanisms, such as
text-to-speech, haptic feedback, and trackball/d-pad navigation.

*   [H-SR] Android Handheld device implementations MUST support third-party
    accessibility services.

*   [W-SR] Android Watch device implementations that declare the
    `android.hardware.audio.output` feature flag MUST support third-party
    accessibility services.

*   [T-SR] Android Television device implementations MUST support third-party
    accessibility services.

*   [A-SR] Android Automotive implementations are STRONGLY RECOMMENDED to
    support third-party accessibility services.

If device implementations support third-party accessibility services, they:

*   [C-1-1] MUST provide an implementation of the Android accessibility
    framework as described in the [accessibility APIs](
    http://developer.android.com/reference/android/view/accessibility/package-summary.html)
    SDK documentation.
*   [C-1-2] MUST generate accessibility events and deliver the appropriate
    `AccessibilityEvent` to all registered [`AccessibilityService`](
    http://developer.android.com/reference/android/accessibilityservice/AccessibilityService.html)
    implementations as documented in the SDK.
*   [C-1-3] MUST honor the `android.settings.ACCESSIBILITY_SETTINGS` intent to
    provide a user-accessible mechanism to enable and disable the third-party
    accessibility services alongside the preloaded accessibility services.
*   [C-1-4] MUST add a button in the system's navigation bar allowing the user
    to control the accessibility service when the enabled accessibility services
    declare the [`AccessibilityServiceInfo.FLAG_REQUEST_ACCESSIBILITY_BUTTON`](
    https://developer.android.com/reference/android/accessibilityservice/AccessibilityServiceInfo.html#FLAG%5FREQUEST%5FACCESSIBILITY%5FBUTTON)
    . Note that for device implementations with no system navigation bar, this
    requirement is not applicable, but device implementations SHOULD provide a
    user affordance to control these accessibility services.

*   [H-SR] Android Handheld device implementations are STRONGLY RECOMMENDED to
  preload accessibility services on the device comparable with or exceeding
  functionality of the Switch Access and TalkBack (for languages supported by
  the preloaded Text-to-speech engine) accessibility services as provided in
  the [talkback open source project](https://github.com/google/talkback).
*   [T-SR] Android Television device implementations are STRONGLY RECOMMENDED to
  preload accessibility services on the device comparable with or exceeding
  functionality of the Switch Access and TalkBack (for languages supported by
  the preloaded Text-to-speech engine) accessibility services as provided in
  the [talkback open source project](https://github.com/google/talkback).
*   [W-SR] Android Watch device implementations that declare `android.hardware.
  audio.output` are STRONGLY RECOMMENDED to preload accessibility services on
  the device comparable with or exceeding functionality of the Switch Access and
  TalkBack (for languages supported by the preloaded Text-to-speech engine)
  accessibility services as provided in the [talkback open source project](
  https://github.com/google/talkback).

If device implementations include preloaded accessibility services, they:

*   [C-2-1] MUST implement these preloaded accessibility services as [Direct Boot aware]
    (https://developer.android.com/reference/android/content/pm/ComponentInfo.html#directBootAware)
    apps when the data storage is encrypted with File Based Encryption (FBE).
*   SHOULD provide a mechanism in the out-of-box setup flow for users to enable
    relevant accessibility services, as well as options to adjust the font size,
    display size and magnification gestures.
