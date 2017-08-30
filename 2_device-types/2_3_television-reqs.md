## 2.3\. Television Requirements

An **Android Television device** refers to an Android device implementation that
is an entertainment interface for consuming digital media, movies, games, apps,
and/or live TV for users sitting about ten feet away (a “lean back” or “10-foot
user interface”).

Android device implementations are classified as a Television if they meet all
the following criteria:

*   Have provided a mechanism to remotely control the rendered user interface on
    the display that might sit ten feet away from the user.
*   Have an embedded screen display with the diagonal length larger than 24
    inches OR include a video output port, such as VGA, HDMI, DisplayPort or a
    wireless port for display.

The additional requirements in the rest of this section are specific to Android
Television device implementations.

### 2.3.1\. Hardware

**Non-touch Navigation (Section 7.2.2)**

Television device implementations:

*    [T-0-1] MUST support [D-pad](https://developer.android.com/reference/android/content/res/Configuration.html#NAVIGATION_DPAD).

**Navigation Keys (Section 7.2.3)**

Television device implementations:

*   [T-0-1] MUST provide the Home and Back functions.
*   [T-0-2] MUST send both the normal and long press event of the the Back
    function
    ([`KEYCODE_BACK`](http://developer.android.com/reference/android/view/KeyEvent.html#KEYCODE_BACK))
    to the foreground application.

**Button Mappings (Section 7.2.6.1)**

Television device implementations:

*    [T-0-1] MUST include support for game controllers and declare the
`android.hardware.gamepad` feature flag.

**Remote Control (Section 7.2.7)**

Television device implementations:

*    SHOULD provide a remote control from which users can access
[non-touch navigation](#7_2_2_non-touch_navigation) and
[core navigation keys](#7_2_3_navigation_keys) inputs.

**Gyroscope (Section 7.3.4)**

If Television device implementations include a gyroscope, they:

*   [T-1-1] MUST be able to report events up to a frequency of at least 100 Hz.

**Bluetooth (Section 7.4.3)**

Television device implementations:

*    [T-0-1] MUST support Bluetooth and Bluetooth LE.

**Minimum Memory and Storage (Section 7.6.1)**

Television device implementations:

*   [T-0-1] MUST have at least 4GB of non-volatile storage available for
    application private data (a.k.a. "/data" partition)

**Microphone (Section 7.8.1)**

Television device implementations:

*   SHOULD include a microphone.

**Audio Output (Section 7.8.2)**

Television device implementations:

*   [T-0-1] MUST have an audio output and declare
    `android.hardware.audio.output`.

### 2.3.2\. Multimedia

**Audio Encoding (Section 5.1)**

Television device implementations MUST support the following audio encoding:

*    [T-0-1] MPEG-4 AAC Profile (AAC LC)
*    [T-0-2] MPEG-4 HE AAC Profile (AAC+)
*    [T-0-3] AAC ELD (enhanced low delay AAC)


**Video Encoding (Section 5.2)**

Television device implementations MUST support the following video encoding:

*    [T-0-1] H.264 AVC
*    [T-0-2] VP8

**H-264 (Section 5.2.2)**

Television device implementations are:

*   [T-SR] STRONGLY RECOMMENDED to support H.264 encoding of 720p and 1080p
resolution videos.
*   [T-SR] STRONGLY RECOMMENDED to support H.264 encoding of 1080p resolution
video at 30 frame-per-second (fps).

**Video Decoding (Section 5.3)**

Television device implementations MUST support the following video decoding:

*    [T-0-1] H.264 AVC
*    [T-0-2] H.265 HEVC
*    [T-0-3] MPEG-4 SP
*    [T-0-4] VP8
*    [T-0-5] VP9

Television device implementations are STRONGLY RECOMMENDED to support the
following video decoding:

*    [T-SR] MPEG-2

**H.264 (Section 5.3.4)**

If Television device implementations support H.264 decoders, they:

*   [T-1-1] MUST support High Profile Level 4.2 and the HD 1080p (at 60 fps)
decoding profile.
*   [T-1-2] MUST be capable of decoding videos with both HD profiles as
indicated in the following table and encoded with either the Baseline Profile,
Main Profile, or the High Profile Level 4.2

**H.265 (HEVC) (Section 5.3.5)**

If Television device implementations support H.265 codec and the HD 1080p
decoding profile, they:

*   [T-1-1] MUST support the Main Profile Level 4.1 Main tier.
*   [T-SR]  Are STRONGLY RECOMMENDED to support 60 fps video frame rate
for HD 1080p.

If Television device implementations support H.265 codec and the UHD decoding
profile, then:

*   [T-2-1] The codec MUST support Main10 Level 5 Main Tier profile.

**VP8 (Section 5.3.6)**

If Television device implementations support VP8 codec, they:

*   [T-1-1] MUST support the HD 1080p60 decoding profile.

If Television device implementations support VP8 codec and support 720p, they:

*   [T-2-1] MUST support the HD 720p60 decoding profile.


**VP9 (Section 5.3.7)**

If Television device implementations support VP9 codec and the UHD video
decoding, they:

*   [T-1-1] MUST support 8-bit color depth and SHOULD support VP9 Profile 2
(10-bit).

If Television device implementations support VP9 codec, the 1080p profile and
VP9 hardware decoding, they:

*   [T-2-1] MUST support 60 fps for 1080p.

**Secure Media (Section 5.8)**

If device implementations are Android Television devices and support 4K
resolution, they:

*    [T-1-1] MUST support HDCP 2.2 for all wired external displays.

If Television device implementations don't support 4K resolution, they:

*    [T-2-1] MUST support HDCP 1.4 for all wired external displays.

Television device implementations:

*    [T-SR] Are STRONGLY RECOMMENDED to support simulataneous decoding of secure
     streams. At minimum, simultaneous decoding of two steams is STRONGLY
     RECOMMENDED.

**Audio Output Volume (Section 5.5.3)**

Television device implementations:

*   [T-0-1] MUST include support for system Master Volume and digital audio
output volume attenuation on supported outputs,
except for compressed audio passthrough output (where no audio decoding is done
on the device).


### 2.3.3\. Software

Television device implementations:

*    [T-0-1] MUST declare the features
     [`android.software.leanback`](http://developer.android.com/reference/android/content/pm/PackageManager.html#FEATURE_LEANBACK)
     and `android.hardware.type.television`.

**WebView compatibility (Section 3.4.1)**

Television device implementations:

*    [T-0-1] MUST provide a complete implementation of the `android.webkit.Webview` API.


**Lock Screen Media Control (Section 3.8.10)**

If Android Television device implementations support a lock screen,they:

*   [T-1-1] MUST display the Lock screen Notifications including the Media Notification Template.

**Multi-windows (Section 3.8.14)**

Television device implementations:

*   [T-SR] Are STRONGLY RECOMMENDED to support picture-in-picture (PIP) mode
    multi-window.

**Accessibility (Section 3.10)**

Television device implementations:

*   [T-SR] MUST support third-party accessibility services.

*   [T-SR] Android Television device implementations are STRONGLY RECOMMENDED to
    preload accessibility services on the device comparable with or exceeding
    functionality of the Switch Access and TalkBack (for languages supported by
    the preloaded Text-to-speech engine) accessibility services as provided in
    the [talkback open source project](https://github.com/google/talkback).

**Text-to-Speech (Section 3.11)**

If device implementations report the feature android.hardware.audio.output,
they:

*   [T-SR] STRONGLY RECOMMENDED to include a TTS engine supporting the
    languages available on the device.

*   [T-0-1] MUST support installation of third-party TTS engines.


**TV Input Framework (Section 3.12)**

Television device implementations:

*    [T-0-1] MUST support TV Input Framework.


### 2.2.4\. Performance and Power


**User Experience Consistency (Section 8.1)**

For Television device implementations:

   *   [T-0-1] **Consistent frame latency**. Inconsistent frame latency or a
delay to render frames MUST NOT happen more often than 5 frames in a second,
and SHOULD be below 1 frames in a second.

**File I/O Access Performance (Section 8.2)**

Television device implementations:

   *   [T-0-1] MUST ensure a sequential write performance of at least 5MB/s.
   *   [T-0-2] MUST ensure a random write performance of at least 0.5MB/s.
   *   [T-0-3] MUST ensure a sequential read performance of at least 15MB/s.
   *   [T-0-4] MUST ensure a random read performance of at least 3.5MB/s.

**Power-Saving Modes (Section 8.3)**

For Television device implementations:

*   [T-0-1] All Apps exempted from App Standby and Doze power-saving modes
MUST be made visible to the end user.
*   [T-0-2] The triggering, maintenance, wakeup algorithms and the use of
global system settings of App Standby and Doze power-saving modes MUST not
deviate from the Android Open Source Project.

**Power Consumption Accounting (Sections 8.4)**

Television device implementations:

*    [T-0-1] MUST provide a per-component power profile that defines the
[current consumption value](
http://source.android.com/devices/tech/power/values.html)
for each hardware component and the approximate battery drain caused by the
components over time as documented in the Android Open Source Project site.
*    [T-0-2] MUST report all power consumption values in milliampere
hours (mAh).
*    [T-0-3] MUST report CPU power consumption per each process's UID.
The Android Open Source Project meets the requirement through the
`uid_cputime` kernel module implementation.
*    SHOULD be attributed to the hardware component itself if unable to
attribute hardware component power usage to an application.
*   [T-0-4] MUST make this power usage available via the
[`adb shell dumpsys batterystats`](
http://source.android.com/devices/tech/power/batterystats.html)
shell command to the app developer.
