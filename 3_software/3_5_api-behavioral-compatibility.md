## 3.5\. API Behavioral Compatibility

The behaviors of each of the API types (managed, soft, native, and web) must be
consistent with the preferred implementation of the upstream
[Android Open Source Project](http://source.android.com/). Some specific areas of
compatibility are:

*   Devices MUST NOT change the behavior or semantics of a standard intent.
*   Devices MUST NOT alter the lifecycle or lifecycle semantics of a particular
    type of system component (such as Service, Activity, ContentProvider, etc.).
*   Devices MUST NOT change the semantics of a standard permission.
*   Devices MUST NOT alter the limitations enforced on background applications.
    More specifically, for background apps:
  *   it MUST stop executing callbacks that are registered to receive outputs from
      the [`GnssMeasurement`](
      https://developer.android.com/reference/android/location/GnssMeasurement.html)
      and [`GnssNavigationMessage`](
      https://developer.android.com/reference/android/location/GnssNavigationMessage.html)
      .
  *   it MUST rate-limit the frequency updates that are provided through the
      [`LocationManager`](
      https://developer.android.com/reference/android/location/LocationManager.html)
      API class or the [`WifiManager.startScan()`](
      https://developer.android.com/reference/android/net/wifi/WifiManager.html#startScan%28%29)
      method.
  *   if the app is targeting API level 25 or higher, it MUST NOT allow to
      register broadcast receivers for the implicit broadcasts of standard
      Android intents in their manifest, unless the broadcst intent requires a
      `"signature"` or `"signatureOrSystem"` [`protectionLevel`](
      https://developer.android.com/guide/topics/manifest/permission-element.html#plevel)
      permission or are on the [exemption list](
      https://developer.android.com/preview/features/background-broadcasts.html).
  *   if the app is targeting API level 25 or higher, it MUST stop the app's
      background services, just as if the app had called the services'
      [`stopSelf()`](
      https://developer.android.com/reference/android/app/Service.html#stopSelf%28%29)
      method, unless the app is placed on a temporary whitelist to handle a task
      that's visible to the user.
  *   if the app is targeting API level 25 higher, it MUST release the wakelocks
      the app holds.

The above list is not comprehensive. The Compatibility Test Suite (CTS) tests
significant portions of the platform for behavioral compatibility, but not all.
It is the responsibility of the implementer to ensure behavioral compatibility
with the Android Open Source Project. For this reason, device implementers
SHOULD use the source code available via the Android Open Source Project where
possible, rather than re-implement significant parts of the system.
