## 2.6\. Tablet Requirements

An **Android Tablet device** refers to an Android device implementation that
typically meets all the following criteria:

*   Used by holding in both hands.
*   Does not have a clamshell or convertible configuration.
*   Physical keyboard implementations used with the device connect by
    means of a standard connection (e.g. USB, Bluetooth).
*   Has a power source that provides mobility, such as a battery.
*   Has a physical diagonal screen size in the range of 7 to 18 inches.

Tablet device implementations have similar requirements to handheld device
implementations. The exceptions are indicated by an \* in that section
and noted for reference in this section.

### 2.6.1\. Hardware

**Screen Size**

*   [[7.1](#7_1_display_and_graphics).1.1/Tab-0-1] MUST have a screen in the
range of 7 to 18 inches.

** Gyroscope**

If Tablet device implementations include a 3-axis gyroscope, they:

*   [[7.3](#7_3_sensors).4/Tab-1-1] MUST be capable of measuring orientation
changes up to 1000 degrees per second.

**Minimum Memory and Storage (Section 7.6.1)**

The screen densities listed for small/normal screens in the handheld
requirements are not applicable to tablets.

**USB peripheral mode (Section 7.7.1)**

If tablet device implementations include a USB port supporting peripheral
mode, they:

*   [[7.7.1](#7_7_usb)/Tab] MAY implement the Android Open Accessory (AOA) API.

**Virtual Reality Mode (Section 7.9.1)**

**Virtual Reality High Performance (Section 7.9.2)**

Virtual reality requirements are not applicable to tablets.

### 2.6.2\. Security Model

**Keys and Credentials (Section 9.11)**

Refer to Section [[9.11](#9_11_permissions)].

If Tablet device implementations include multiple users and
do not declare the `android.hardware.telephony` feature flag, they:

*   [[9.5](#9_5_multi-user-support)/T-1-1] MUST support restricted profiles,
    a feature that allows device owners to manage additional users and their
    capabilities on the device. With restricted profiles, device owners can
    quickly set up separate environments for additional users to work in,
    with the ability to manage finer-grained restrictions in the apps that
    are available in those environments.

If Tablet device implementations include multiple users and
declare the `android.hardware.telephony` feature flag, they:

*   [[9.5](#9_5_multi-user-support)/T-2-1] MUST NOT support restricted
    profiles but MUST align with the AOSP implementation of controls
    to enable /disable other users from accessing the voice calls and SMS.

### 2.6.2\. Software

*   [[3.2.3.1](#3_2_3_1_common_application_intents)/Tab-0-1]  MUST preload one
or more applications or service components with an intent handler, for all the
public intent filter patterns defined by the following application intents
listed [here](https://developer.android.com/about/versions/11/reference/common-intents-30).
