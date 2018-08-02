## 8.3\. Power-Saving Modes

Android includes App Standby and Doze power-saving modes to optimize battery
usage.
*   [SR] All Apps exempted from these modes are STRONGLY RECOMMENDED to be made
visible to the end user.
*   [SR] The triggering, maintenance, wakeup algorithms and the use of
global system settings of these power-saving modes are STRONGLY RECOMMENDED NOT
to deviate from the Android Open Source Project.

In addition to the power-saving modes, Android device implementations MAY
implement any or all of the 4 sleeping power states as defined by the Advanced
Configuration and Power Interface (ACPI).

If device implementations implement S3 and S4 power states as defined by the
ACPI, they:

*   [C-1-1] MUST enter these states only after the user has taken an explicit action
    to put the device in an inactive state (e.g. by closing a lid that is physically
    part of the device or turning off a vehicle or television) and before the user re-activates the
    device (e.g. by opening the lid or turning the vehicle or television back on).