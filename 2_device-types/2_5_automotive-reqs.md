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

Automotive device implementations:

*   [[7.1](#7_1_display_and-graphics).1.1/A-0-1] MUST have a screen at least 6
inches in physical diagonal size.
*   [[7.1](#7_1_display_and_graphics).1.1/A-0-2] MUST have a screen size layout
of at least 750 dp x 480 dp.

*   [[7.2](#7_2_input_devices).3/A-0-1] MUST provide the Home function and MAY
provide Back and Recent functions.
*   [[7.2](#7_2_input_devices).3/A-0-2] MUST send both the normal and long press
event of the Back function ([`KEYCODE_BACK`](
http://developer.android.com/reference/android/view/KeyEvent.html#KEYCODE_BACK))
to the foreground application.
*   [[7.3](#7_3_sensors)/A-0-1] MUST implement and report
[`GEAR_SELECTION`](https://developer.android.com/reference/android/car/VehiclePropertyIds.html#GEAR_SELECTION),
[`NIGHT_MODE`](https://developer.android.com/reference/android/car/VehiclePropertyIds.html#NIGHT_MODE),
[`PERF_VEHICLE_SPEED`](https://developer.android.com/reference/android/car/VehiclePropertyIds.html#PERF_VEHICLE_SPEED)
and [`PARKING_BRAKE_ON`](https://developer.android.com/reference/android/car/VehiclePropertyIds.html#PARKING_BRAKE_ON).
*    [[7.3](#7_3_sensors)/A-0-2] The value of the
[`NIGHT_MODE`](https://developer.android.com/reference/android/car/VehiclePropertyIds.html#NIGHT_MODE)
flag MUST be consistent with dashboard day/night mode and SHOULD be based on
ambient light sensor input. The underlying ambient light sensor MAY be the same
as [Photometer](#7_3_7_photometer).
*   [[7.3](#7_3_sensors).1/A-SR] Are STRONGLY RECOMMENDED to include a 3-axis
accelerometer.

If Automotive device implementations include a 3-axis accelerometer, they:

*   [[7.3](#7_3_sensors).1/A-1-1] MUST be able to report events up to a
frequency of at least 100 Hz.
*   [[7.3](#7_3_sensors).1/A-1-2] MUST comply with the Android
[car sensor coordinate system](
http://source.android.com/devices/sensors/sensor-types.html#auto_axes).

If Automotive device implementations include a gyroscope, they:

*   [[7.3](#7_3_sensors).4/A-1-1] MUST be able to report events up to a
frequency of at least 100 Hz.
*   [[7.3](#7_3_sensors).4/A-1-2] MUST also implement the
[`TYPE_GYROSCOPE_UNCALIBRATED`](https://developer.android.com/reference/android/hardware/Sensor.html#TYPE_GYROSCOPE_UNCALIBRATED)
sensor.


Automotive device implementations:
*    [[7.4](#7_4_data_connectivity).3/A-0-1] MUST support Bluetooth and SHOULD
support Bluetooth LE.
*    [[7.4](#7_4_data_connectivity).3/A-0-2] Android Automotive implementations
MUST support the following Bluetooth profiles:
     * Phone calling over Hands-Free Profile (HFP).
     * Media playback over Audio Distribution Profile (A2DP).
     * Media playback control over Remote Control Profile (AVRCP).
     * Contact sharing using the Phone Book Access Profile (PBAP).
*    [[7.4](#7_4_data_connectivity).3/A-SR] Are STRONGLY RECOMMENDED to support
Message Access Profile (MAP).

*   [[7.4](#7_4_data_connectivity).5/A] SHOULD include support for cellular
network-based data connectivity.
*   [[7.4](#7_4_data_connectivity).5/A] MAY use the System API
`NetworkCapabilities#NET_CAPABILITY_OEM_PAID` constant for
networks that should be available to system apps.

*   [[7.6](#7_6_memory_and_storage).1/A-0-1] MUST have at least 4 GB of
non-volatile storage available for application private data
(a.k.a. "/data" partition).

Automotive device implementations:

*   [[7.6](#7_6_memory_and_storage).1/A] SHOULD format the data partition
to offer improved performance and longevity on flash storage, for example
using `f2fs` file-system.

If Automotive device implementations provide shared external storage via a
portion of the internal non-removable storage, they:

*   [[7.6](#7_6_memory_and_storage).1/A-SR] Are STRONGLY RECOMMENDED to reduce
I/O overhead on operations performed on the external storage, for example by
using `SDCardFS`.

If Automotive device implementations are 32-bit:

*   [[7.6](#7_6_memory_and_storage).1/A-1-1] The memory available to the kernel
and userspace MUST be at least 512MB if any of the following densities are used:
     *    280dpi or lower on small/normal screens
     *    ldpi or lower on extra large screens
     *    mdpi or lower on large screens

*   [[7.6](#7_6_memory_and_storage).1/A-1-2] The memory available to the kernel
and userspace MUST be at least 608MB if any of the following densities are used:
     *   xhdpi or higher on small/normal screens
     *   hdpi or higher on large screens
     *   mdpi or higher on extra large screens

*   [[7.6](#7_6_memory_and_storage).1/A-1-3] The memory available to the kernel
and userspace MUST be at least 896MB if any of the following densities are used:
     *   400dpi or higher on small/normal screens
     *   xhdpi or higher on large screens
     *   tvdpi or higher on extra large screens

*   [[7.6](#7_6_memory_and_storage).1/A-1-4] The memory available to the kernel
and userspace MUST be at least 1344MB if any of the following densities are
used:
     *   560dpi or higher on small/normal screens
     *   400dpi or higher on large screens
     *   xhdpi or higher on extra large screens

If Automotive device implementations are 64-bit:

*   [[7.6](#7_6_memory_and_storage).1/A-2-1] The memory available to the kernel
and userspace MUST be at least 816MB if any of the following densities are used:
     *   280dpi or lower on small/normal screens
     *   ldpi or lower on extra large screens
     *   mdpi or lower on large screens

*   [[7.6](#7_6_memory_and_storage).1/A-2-2] The memory available to the kernel
and userspace MUST be at least 944MB if any of the following densities are used:
     *   xhdpi or higher on small/normal screens
     *   hdpi or higher on large screens
     *   mdpi or higher on extra large screens

*   [[7.6](#7_6_memory_and_storage).1/A-2-3] The memory available to the kernel
and userspace MUST be at least 1280MB if any of the following densities are used:
     *  400dpi or higher on small/normal screens
     *  xhdpi or higher on large screens
     *  tvdpi or higher on extra large screens

*   [[7.6](#7_6_memory_and_storage).1/A-2-4] The memory available to the kernel
and userspace MUST be at least 1824MB if any of the following densities are used:
     *   560dpi or higher on small/normal screens
     *   400dpi or higher on large screens
     *   xhdpi or higher on extra large screens

Note that the "memory available to the kernel and userspace" above refers to the
memory space provided in addition to any memory already dedicated to hardware
components such as radio, video, and so on that are not under the kernel’s
control on device implementations.

Automotive device implementations:

*   [[7.7](#7_7_usb).1/A] SHOULD include a USB port supporting peripheral mode.

Automotive device implementations:

*   [[7.8](#7_8_audio).1/A-0-1] MUST include a microphone.

Automotive device implementations:

*   [[7.8](#7_8_audio).2/A-0-1] MUST have an audio output and declare
    `android.hardware.audio.output`.

### 2.5.2\. Multimedia

Automotive device implementations MUST support the following audio encoding:

*    [[5.1](#5_1_media_codecs)/A-0-1] MPEG-4 AAC Profile (AAC LC)
*    [[5.1](#5_1_media_codecs)/A-0-2] MPEG-4 HE AAC Profile (AAC+)
*    [[5.1](#5_1_media_codecs)/A-0-3] AAC ELD (enhanced low delay AAC)

Automotive device implementations MUST support the following video encoding:

*    [[5.2](#5_2_video_encoding)/A-0-1] H.264 AVC
*    [[5.2](#5_2_video_encoding)/A-0-2] VP8

Automotive device implementations MUST support the following video decoding:

*    [[5.3](#5_3_video_decoding)/A-0-1] H.264 AVC
*    [[5.3](#5_3_video_decoding)/A-0-2] MPEG-4 SP
*    [[5.3](#5_3_video_decoding)/A-0-3] VP8
*    [[5.3](#5_3_video_decoding)/A-0-4] VP9

Automotive device implementations are STRONGLY RECOMMENDED to support the
following video decoding:

*    [[5.3](#5_3_video_decoding)/A-SR] H.265 HEVC


### 2.5.3\. Software

Automotive device implementations:

*   [[3](#3_0_intro)/A-0-1] MUST declare the feature
`android.hardware.type.automotive`.

*   [[3](#3_0_intro)/A-0-2] MUST support uiMode = [`UI_MODE_TYPE_CAR`](
http://developer.android.com/reference/android/content/res/Configuration.html#UI_MODE_TYPE_CAR).

*   [[3](#3_0_intro)/A-0-3] MUST support all public APIs in the
[`android.car.*`](https://developer.android.com/reference/android/car/package-summary)
namespace.

*   [[3.4](#3_4_web_compatibility).1/A-0-1] MUST provide a complete
implementation of the `android.webkit.Webview` API.

*   [[3.8](#3_8_user_interface_compatibility).3/A-0-1] MUST display
notifications that use the [`Notification.CarExtender`](
https://developer.android.com/reference/android/app/Notification.CarExtender.html)
API when requested by third-party applications.

*   [[3.8](#3_8_user_interface_compatibility).4/A-0-1] MUST implement an
assistant on the device that provides a default implementation of the
[`VoiceInteractionSession`](https://developer.android.com/reference/android/service/voice/VoiceInteractionSession)
service.

*   [[3.13](#3_13_quick_settings)/A-SR] Are STRONGLY RECOMMENDED to include a
Quick Settings UI component.

If Automotive device implementations include a push-to-talk button, they:

*   [[3.8](#3_8_user_interface_compatibility).4/A-1-1] MUST use a short press of
the push-to-talk button as the designated interaction to launch the
user-selected assist app, in other words the app that implements
[`VoiceInteractionService`](
https://developer.android.com/reference/android/service/voice/VoiceInteractionService).

Automotive device implementations:

*   [[3.14](#3_14_media_ui)/A-0-1] MUST include a UI framework to support
third-party apps using the media APIs as described in section
[3.14](#3_14_media_ui).

### 2.5.4\. Performance and Power

If Automotive device implementations include features to improve device power
management that are included in AOSP or extend the features that are included
in AOSP, they:

* [[8.3](#8_3_power_saving_modes)/A-1-1] MUST provide user affordance to enable
  and disable the battery saver feature.
* [[8.3](#8_3_power_saving_modes)/A-1-2] MUST provide user affordance to display
  all apps that are exempted from App Standby and Doze power-saving modes.

Automotive device implementations:

*   [[8.2](#8_2_file_i/o_access_performance)/A-0-1] MUST report the number of
bytes read and written to non-volatile storage per each process's UID so the
stats are available to developers through System API
`android.car.storagemonitoring.CarStorageMonitoringManager`. The Android Open
Source Project meets the requirement through the `uid_sys_stats` kernel module.
*   [[8.4](#8_4_power_consumption_accounting)/A-0-1] MUST provide a
per-component power profile that defines the [current consumption value](
http://source.android.com/devices/tech/power/values.html)
for each hardware component and the approximate battery drain caused by the
components over time as documented in the Android Open Source Project site.
*   [[8.4](#8_4_power_consumption_accounting)/A-0-2] MUST report all power
consumption values in milliampere hours (mAh).
*   [[8.4](#8_4_power_consumption_accounting)/A-0-3] MUST report CPU power
consumption per each process's UID. The Android Open Source Project meets the
requirement through the `uid_cputime` kernel module implementation.
*   [[8.4](#8_4_power_consumption_accounting)/A] SHOULD be attributed to the
hardware component itself if unable to attribute hardware component power usage
to an application.
*   [[8.4](#8_4_power_consumption_accounting)/A-0-4] MUST make this power usage
available via the [`adb shell dumpsys batterystats`](
http://source.android.com/devices/tech/power/batterystats.html)
shell command to the app developer.

### 2.5.5\. Security Model


If Automotive device implementations support multiple users, they:

*   [[9.5](#9_5_multi_user_support)/A-1-1] MUST include a guest account that
allows all functions provided by the vehicle system without requiring a user to
log in.

If Automotive device implementations support a secure lock screen, they:

*   [[9.9](#9_9_full_disk_encryption).2/A-1-1] MUST support encryption per
user-specific authentication keys. [File-Based Encryption (FBE)](
https://source.android.com/security/encryption/file-based) is one way to do it.

Automotive device implementations:

*   [[9.14](#9_14_automotive_system_isolation)/A-0-1] MUST gatekeep messages
from Android framework vehicle subsystems, e.g., whitelisting permitted message
types and message sources.
*   [[9.14](#9_14_automotive_system_isolation)/A-0-2] MUST watchdog against
denial of service attacks from the Android framework or third-party apps. This
guards against malicious software flooding the vehicle network with traffic,
which may lead to malfunctioning vehicle subsystems.
