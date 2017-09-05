## 2.4\. Watch Requirements

An **Android Watch device** refers to an Android device implementation intended to
be worn on the body, perhaps on the wrist.

Android device implementations are classified as a Watch if they meet all the
following criteria:

*   Have a screen with the physical diagonal length in the range from 1.1 to 2.5
    inches.
*   Have a mechanism provided to be worn on the body.

The additional requirements in the rest of this section are specific to Android
Watch device implementations.

### 2.4.1\. Hardware

**Screen Size (Section 7.1.1.1)**

Watch device implementations:

*   [W-0-1] MUST have a screen with the physical diagonal size in the range from
    1.1 to 2.5 inches.

**Navigation Keys (Section 7.2.3)**

Watch device implementations:

*   [W-0-1] MUST have the Home function available to the user, and the Back
    function except for when it is in `UI_MODE_TYPE_WATCH`.

**Touchscreen Input (Section 7.2.4)**

Watch device implementations:

*    [W-0-2] MUST support touchscreen input.

**Accelerometer (Section 7.3.1)**

Watch device implementations:

*   [W-SR] Are STRONGLY RECOMMENDED to include a 3-axis accelerometer.

**Bluetooth (Section 7.4.3)**

Watch device implementations:

*    [W-0-1] MUST support Bluetooth.


**Minimum Memory and Storage (Section 7.6.1)**

Watch device implementations:

*   [W-0-1] MUST have at least 1GB of non-volatile storage available for
    application private data (a.k.a. "/data" partition)
*   [W-0-2] MUST have at least 416MB memory available to the kernel and
    userspace.

**Microphone (Section 7.8.1)**

Watch device implementations:

*    [W-0-1] MUST include a microphone.

**Audio Output (Section 7.8.1)**

Watch device implementations:

*   MAY but SHOULD NOT have audio output.

### 2.4.2\. Multimedia

No additional requirements.

### 2.4.3\. Software

Watch device implementations:

*   [W-0-1] MUST declare the feature android.hardware.type.watch.
*   [W-0-2] MUST support uiMode =
    [UI_MODE_TYPE_WATCH](http://developer.android.com/reference/android/content/res/Configuration.html#UI_MODE_TYPE_WATCH).


**Search (Section 3.8.4)**

Watch device implementations:

*   [W-SR] Are STRONGLY RECOMMENDED to implement an assistant on the device to
    handle the [Assist action](
    http://developer.android.com/reference/android/content/Intent.html#ACTION_ASSIST).


**Accessibility (Section 3.10)**

Watch device implementations that declare the `android.hardware.audio.output` feature flag:

*   [W-1-1]  MUST support third-party accessibility services.

*   [W-SR] Are STRONGLY RECOMMENDED to preload accessibility services on
    the device comparable with or exceeding functionality of the Switch Access
    and TalkBack (for languages supported by the preloaded Text-to-speech
    engine) accessibility services as provided in the [talkback open source
    project]( https://github.com/google/talkback).

**Text-to-Speech (Section 3.11)**

If Watch device implementations report the feature android.hardware.audio.output,
they:

*   [W-SR] Are STRONGLY RECOMMENDED to include a TTS engine supporting the
    languages available on the device.

*   [W-0-1] MUST support installation of third-party TTS engines.
