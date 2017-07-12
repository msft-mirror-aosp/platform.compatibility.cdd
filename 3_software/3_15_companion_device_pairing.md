## 3.15\. Companion Device Pairing

Android includes support for companion device pairing to more effectively manage
association with companion devices and provides the [`CompanionDeviceManager`
](https://developer.android.com/reference/android/companion/CompanionDeviceManager.html)
API for apps to access this feature.

Handheld devices declaring `FEATURE_BLUETOOTH` or `FEATURE_WIFI` support, MUST
also support the companion device pairing feature.

If a device implementation supports the companion device pairing feature, it:

*   MUST declare the feature flag [`FEATURE_COMPANION_DEVICE_SETUP`
    ](https://developer.android.com/reference/android/content/pm/PackageManager.html?#FEATURE_COMPANION_DEVICE_SETUP)
    .
*   MUST ensure the APIs in the [`android.companion`
    ](https://developer.android.com/reference/android/companion/package-summary.html)
    package is fully implemented.
*   MUST provide user affordances for the user to select/confirm a companion
    device is present and operational.
