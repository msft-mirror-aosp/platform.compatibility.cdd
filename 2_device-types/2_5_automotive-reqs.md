## 2.5\. Automotive Requirements

**Android Automotive implementation** refers to a vehicle head unit running
Android as an operating system for part or all of the system and/or
infotainment functionality.

Android device implementations are classified as an Automotive if they declare
the feature `android.hardware.type.automotive` or meet all the following
criteria.

*   Are embedded as part of, or pluggable to, an automotive vehicle.
*   Are using a screen in the driver's seat row as the primary display.

The additional requirements in the rest of this section are specific to Android
Automotive device implementations.

### 2.5.1\. Hardware

**Screen Size (Section 7.1.1.1)**

Automotive device implementations:

*   [A-0-1] MUST have a screen at least 6 inches in physical diagonal size.
*   [A-0-2] MUST have a screen size layout of at least 750 dp x 480 dp.

**Navigation Keys (Section 7.2.3)**

Automotive device implementations:

*   [A-0-1] MUST provide the Home function and MAY provide Back and Recent
    functions.
*   [A-0-2] MUST send both the normal and long press event of the the Back
    function
    ([`KEYCODE_BACK`](http://developer.android.com/reference/android/view/KeyEvent.html#KEYCODE_BACK))
    to the foreground application.

**Accelerometer (Section 7.3.1)**

Automotive device implementations:

*   [A-SR] Are STRONGLY RECOMMENDED to include a 3-axis accelerometer.

If Automotive device implementations include a 3-axis accelerometer, they:

*   [A-1-1] MUST be able to report events up to a frequency of at least 100 Hz.
*   [A-1-2] MUST comply with the Android
    [car sensor coordinate system](
    http://source.android.com/devices/sensors/sensor-types.html#auto_axes).

**GPS (Section 7.3.3)**

If Automotive device implementations include a GPS/GNSS receiver and report
the capability to applications through the `android.hardware.location.gps`
feature flag:

*   [A-1-1] GNSS technology generation MUST be the year "2017" or newer.

**Gyroscope (Section 7.3.4)**

If Automotive device implementations include a gyroscope, they:

*   [A-1-1] MUST be able to report events up to a frequency of at least 100 Hz.

**Android Automotive-only sensors (Section 7.3.11)**
**Current Gear (Section 7.3.11.1)**

Automotive device implementations:

*    SHOULD provide current gear as `SENSOR_TYPE_GEAR`.

**Day Night Mode (Section 7.3.11.2)**

Automotive device implementations:

*    [A-0-1] MUST support day/night mode defined as `SENSOR_TYPE_NIGHT`.
*    [A-0-2] The value of the `SENSOR_TYPE_NIGHT` flag MUST be consistent with
     dashboard day/night mode and SHOULD be based on ambient light sensor input.
*    The underlying ambient light sensor MAY be the same as
[Photometer](#7_3_7_photometer).

**Driving Status (Section 7.3.11.3)**

Automotive device implementations:

*    [A-0-1] MUST support driving status defined as
     `SENSOR_TYPE_DRIVING_STATUS`, with a default value of
     `DRIVE_STATUS_UNRESTRICTED` when the vehicle is fully stopped and parked.
     It is the responsibility of device manufacturers to configure
     `SENSOR_TYPE_DRIVING_STATUS` in compliance with all laws and regulations
     that apply to markets where the product is shipping.

**Wheel Speed (Section 7.3.11.4)**

Automotive device implementations:

*    [A-0-1] MUST provide vehicle speed defined as `SENSOR_TYPE_CAR_SPEED`.

**Bluetooth (Section 7.4.3)**

Automotive device implementations:

*    [A-0-1] MUST support Bluetooth and SHOULD support Bluetooth LE.

*    [A-0-2] Android Automotive implementations MUST support the following
     Bluetooth profiles:
     * Phone calling over Hands-Free Profile (HFP).
     * Media playback over Audio Distribution Profile (A2DP).
     * Media playback control over Remote Control Profile (AVRCP).
     * Contact sharing using the Phone Book Access Profile (PBAP).
*    SHOULD support Message Access Profile (MAP).

**Minimum Network Capability (Section 7.4.5)**

Automotive device implementations:

*   SHOULD include support for cellular network based data connectivity.

**Minimum Memory and Storage (Section 7.6.1)**

Automotive device implementations:

*   [A-0-1] MUST have at least 4GB of non-volatile storage available for
    application private data (a.k.a. "/data" partition)

**USB peripheral mode (Section 7.7.1)**

Automotive device implementations:

*   SHOULD include a USB port supporting peripheral mode.

**Microphone (Section 7.8.1)**

Automotive device implementations:

*    [A-0-1] MUST include a microphone.

**Audio Output (Section 7.8.2)**

Automotive device implementations:

*   [A-0-1] MUST have an audio output and declare
    `android.hardware.audio.output`.

### 2.5.2\. Multimedia

**Audio Encoding (Section 5.1)**

Automotive device implementations MUST support the following audio encoding:

*    [A-1-1] MPEG-4 AAC Profile (AAC LC)
*    [A-1-2] MPEG-4 HE AAC Profile (AAC+)
*    [A-1-3] AAC ELD (enhanced low delay AAC)

**Video Encoding (Section 5.2)**

Automotive device implementations MUST support the following video encoding:

*    [A-0-1] H.264 AVC
*    [A-0-2] VP8

**Video Decoding (Section 5.3)**

Automotive device implementations MUST support the following video decoding:

*    [A-0-1] H.264 AVC
*    [A-0-2] MPEG-4 SP
*    [A-0-3] VP8
*    [A-0-4] VP9

Automotive device implementations are STRONGLY RECOMMENDED to support the
following video decoding:

*    [A-SR] H.265 HEVC


### 2.5.3\. Software

Automotive device implementations:

*   [A-0-1] MUST declare the feature android.hardware.type.automotive.
*   [A-0-2] MUST support uiMode =
    [UI_MODE_TYPE_CAR](http://developer.android.com/reference/android/content/res/Configuration.html#UI_MODE_TYPE_CAR).
*   [A-0-3] Android Automotive implementations MUST support all public APIs in the
`android.car.*` namespace.

**WebView Compatibility (Section 3.4.1)**

Automotive device implementations:

*   [A-0-1] MUST provide a complete implementation of the `android.webkit.Webview API`.

**Notifications (Section 3.8.3)**

Android Automotive device implementations:

*   [A-0-1] MUST display notifications that use the [`Notification.CarExtender`](
    https://developer.android.com/reference/android/app/Notification.CarExtender.html) API when
    requested by third-party applications.

**Search (Section 3.8.4)**

Automotive device implementations:

*   [A-0-1] MUST implement an assistant on the device to handle the 
    [Assist action](
    http://developer.android.com/reference/android/content/Intent.html#ACTION_ASSIST).


**Media UI (Section 3.14)**

Automotive device implementations:

*   [A-0-1] MUST include a UI framework to support third-party apps using the
    media APIs as described in section 3.14.

### 2.2.4\. Performance and Power

**Power-Saving Modes (Section 8.3)**

For Automotive device implementations:

*   [A-0-1] All Apps exempted from App Standby and Doze power-saving modes
MUST be made visible to the end user.
*   [A-0-2] The triggering, maintenance, wakeup algorithms and the use of
global system settings of App Standby and Doze power-saving modes MUST not
deviate from the Android Open Source Project.

**Power Consumption Accounting (Sections 8.4)**

Automotive device implementations:

*    [A-0-1] MUST provide a per-component power profile that defines the
[current consumption value](
http://source.android.com/devices/tech/power/values.html)
for each hardware component and the approximate battery drain caused by the
components over time as documented in the Android Open Source Project site.
*    [A-0-2] MUST report all power consumption values in milliampere
hours (mAh).
*    [A-0-3] MUST report CPU power consumption per each process's UID.
The Android Open Source Project meets the requirement through the
`uid_cputime` kernel module implementation.
*    SHOULD be attributed to the hardware component itself if unable to
attribute hardware component power usage to an application.
*   [A-0-4] MUST make this power usage available via the
[`adb shell dumpsys batterystats`](
http://source.android.com/devices/tech/power/batterystats.html)
shell command to the app developer.

### 2.2.5\. Security Model

**Multi-User Support (Section 9.5)**

If Automotive device implementations include multiple users, they:

*   [A-1-1] MUST include a guest account that allows all functions provided
by the vehicle system without requiring a user to log in.

**Automotive Vehicle System Isolation (Section 9.14)**

Automotive device implementations:

*    [A-0-1] MUST gatekeep messages from Android framework vehicle subsystems,
e.g., whitelisting permitted message types and message sources.
*    [A-0-2] MUST watchdog against denial of service attacks from the Android
framework or third-party apps. This guards against malicious software flooding
the vehicle network with traffic, which may lead to malfunctioning vehicle
subsystems.
