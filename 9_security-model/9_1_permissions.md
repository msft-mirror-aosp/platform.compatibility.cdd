## 9.1\. Permissions

Device implementations MUST support the
[Android permissions model](http://developer.android.com/guide/topics/security/permissions.html) as
defined in the Android developer documentation. Specifically, implementations
MUST enforce each permission defined as described in the SDK documentation; no
permissions may be omitted, altered, or ignored. Implementations MAY add
additional permissions, provided the new permission ID strings are not in the
android.\* namespace.

Permissions with a `protectionLevel` of [PROTECTION_FLAG_PRIVILEGED](
https://developer.android.com/reference/android/content/pm/PermissionInfo.html#PROTECTION_FLAG_PRIVILEGED)
MUST only be granted to apps preloaded in the privileged path(s) of the system image and within the
subset of the explicitly whitelisted permissions for each app. The AOSP implementation meets this
requirement by reading and honoring the whitelisted permissions for each app from the files in the
`etc/permissions/` path and using the `system/priv-app` path as the privileged path.

Permissions with a protection level of dangerous are runtime permissions.
Applications with targetSdkVersion > 22 request them at runtime. Device
implementations:

*   MUST show a dedicated interface for the user to decide whether to grant the
requested runtime permissions and also provide an interface for the user to
manage runtime permissions.
*   MUST have one and only one implementation of both user interfaces.
*   MUST NOT grant any runtime permissions to preinstalled apps unless:
    *   the user's consent can be obtained before the application uses it
    *   the runtime permissions are associated with an intent pattern for which
the preinstalled application is set as the default handler

Android Television devices are STRONGLY RECOMMENDED to provide a user-accessible
mechanism to grant or revoke access to the usage stats in response to the
[android.settings.ACTION_USAGE_ACCESS_SETTINGS](https://developer.android.com/reference/android/provider/Settings.html#ACTION_USAGE_ACCESS_SETTINGS)
intent for apps that declare the android.permission.PACKAGE_USAGE_STATS permission.
All other device implementations MUST provide this mechanism unless the implementation
made a conscious design decision to altogether prevent any app, including the
pre-installed apps, from having granted this permission.