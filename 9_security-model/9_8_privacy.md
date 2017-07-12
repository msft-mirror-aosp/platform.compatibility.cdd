## 9.8\. Privacy

If the device implements functionality in the system that captures the contents
displayed on the screen and/or records the audio stream played on the device,
it MUST continuously notify the user whenever this functionality is enabled and
actively capturing/recording.

If a device implementation has a mechanism that routes network data traffic
through a proxy server or VPN gateway by default (for example, preloading a VPN
service with android.permission.CONTROL_VPN granted), the device implementation
MUST ask for the user's consent before enabling that mechanism, unless that
VPN is enabled by the Device Policy Controller via the
[`DevicePolicyManager.setAlwaysOnVpnPackage()`](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setAlwaysOnVpnPackage(android.content.ComponentName, java.lang.String, boolean))
, in which case the user does not need to provide a separate consent, but MUST
only be notified.

Device implementations MUST ship with an empty user-added Certificate Authority
(CA) store, and MUST preinstall the same root certificates for the system-trusted
CA store as [provided](https://source.android.com/security/overview/app-security.html#certificate-authorities)
in the upstream Android Open Source Project.

When device traffic is routed through a VPN, the implementation MUST display a
warning to the user indicating either:

   * That network traffic may be monitored.
   * That network traffic is being routed through the specific VPN application
     providing the VPN.

When a user root CA is installed the implementation MUST display a warning
indicating the network traffic may be monitored to the user.

If a device implementation has a USB port with USB peripheral mode support, it
MUST present a user interface asking for the user's consent before allowing
access to the contents of the shared storage over the USB port.

Android stores the history of the user's choices and manages such history by
[UsageStatsManager](https://developer.android.com/reference/android/app/usage/UsageStatsManager.html)
. Device implementations MUST keep a reasonable retention period of such user
history. It is STRONGLY RECOMMENDED to keep the 14 days retention period as
configured by default in the AOSP implementation.

Device implementations MAY include an Ambient Sound Service component, capable
of recording ambient audio to infer useful information about user’s context
out-of-box, but the recorded raw audio or any format that can be converted back
into the original audio or a near facsimile MUST NOT be stored in persistent
storage or transmitted off the device without explicit user consent.

