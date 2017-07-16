## 9.11\. Keys and Credentials

The [Android Keystore System](https://developer.android.com/training/articles/keystore.html) allows
app developers to store cryptographic keys in a container and use them in
cryptographic operations through the
[KeyChain API](https://developer.android.com/reference/android/security/KeyChain.html) or
the [Keystore API](https://developer.android.com/reference/java/security/KeyStore.html).

All Android device implementations MUST meet the following requirements:

*   SHOULD not limit the number of keys that can be generated, and MUST at
    least allow more than 8,192 keys to be imported.
*   The lock screen authentication MUST rate limit attempts and MUST have an
    exponential backoff algorithm. Beyond 150 failed attempts, the delay MUST be
    at least 24 hours per attempt.
*   When the device implementation supports a secure lock screen it MUST back up the
    keystore implementation with secure hardware and meet following requirements:
    *   MUST have implementations of RSA, AES, ECDSA and HMAC cryptographic
        algorithms and MD5, SHA1, and SHA-2 family hash functions to properly
        support the Android Keystore system's supported algorithms in an area
        that is securely isolated from the code running on the kernel and
        above. Secure isolation MUST block all potential mechanisms by which
        kernel or userspace code might access the internal state of the
        isolated environment, including DMA. The upstream Android Open Source
        Project (AOSP) meets this requirement by using the [Trusty](https://source.android.com/security/trusty/)
        implementation, but another ARM TrustZone-based solution or a
        third-party reviewed secure implementation of a proper
        hypervisor-based isolation are alternative options.
    *   MUST perform the lock screen authentication in the isolated execution
        environment and only when successful, allow the authentication-bound
        keys to be used. The upstream Android Open Source Project provides
        the [Gatekeeper Hardware Abstraction Layer (HAL)](http://source.android.com/devices/tech/security/authentication/gatekeeper.html)
        and Trusty, which can be used to satisfy this requirement.
    *   MUST support key attestation where the attestation signing key is protected by secure
        hardware and signing is performed in secure hardware. The attestation signing keys MUST be
        shared across large enough number of devices to prevent the keys from being used as device
        identifiers. One way of meeting this requirement is to share the same attestation key unless
        at least 100,000 units of a given SKU are produced. If more than 100,000 units of an SKU
        are produced, a different key MAY be used for each 100,000 units.

Note that if a device implementation is already launched on an earlier Android
version, such a device is exempted from the requirement to have a
hardware-backed keystore, unless it declares the `android.hardware.fingerprint`
feature which requires a hardware-backed keystore.

### 9.11.1\. Secure Lock Screen

Device implementations with a secure lock screen MAY include one or more trust
agent, which implements the `TrustAgentService` System API, but it:

*   MUST indicate the user in the Settings and Lock screen user interface of
    situations where either the screen auto-lock is deferred or the screen lock
    can be unlocked by the trust agent. The AOSP meets the requirement by
    showing a text description for the "Automatically lock setting" and
    "Power button instantly locks setting" menus and a distinguishable icon on
    the lock screen.
*   MUST respect and fully implement all trust agent APIs in the
    `DevicePolicyManager` class, such as the [`KEYGUARD_DISABLE_TRUST_AGENTS`
    ](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#KEYGUARD_DISABLE_TRUST_AGENTS)
    constant.

Device implementations MAY add or modify the authentication methods to unlock
the lock screen.

However for such an authentication method to be treated as a secure way to lock
the screen, it:

*   MUST be the user authentication method as described in [Requiring
    User Authentication For Key Use](
    https://developer.android.com/training/articles/keystore.html#UserAuthentication).
*   MUST unlock all keys for a third-party developer app to use when the user unlocks the secure
    lock screen. For example, all keys MUST be available for a third-party developer app through
    relevant APIs, such as
    [`createConfirmDeviceCredentialIntent`](
    https://developer.android.com/reference/android/app/KeyguardManager.html#createConfirmDeviceCredentialIntent%28java.lang.CharSequence, java.lang.CharSequence%29)
    and [`setUserAuthenticationRequired`](
    https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.Builder.html#setUserAuthenticationRequired%28boolean%29).
*   If based on a known secret, MUST meet all following requirements:
    *    The entropy of the shortest allowed length of inputs MUST be greater
         than 10 bits.
    *    The maximum entropy of all possible inputs MUST be greater than 18 bits.
    *    MUST not replace any of the existing authentication methods (PIN,
         pattern, password) implemented and provided in AOSP.
    *    MUST be disabled when the Device Policy Controller (DPC) application
         has set the password quality policy via the
         [`DevicePolicyManager.setPasswordQuality()`](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordQuality%28android.content.ComponentName,%20int%29)
         method with a more restrictive quality constant than `PASSWORD_QUALITY_SOMETHING`.
*   If based on a physical token or the location, MUST meet all following
    requirements:
    *    It MUST have a fall-back mechanism to use one of the primary
         authentication methods which is based on a known secret and meets
         the requirements to be treated as a secure lock screen.
    *    It MUST be disabled and only allow the primary authentication to
         unlock the screen when the Device Policy Controller (DPC) application
         has set the policy with either the
         [`DevicePolicyManager.setKeyguardDisabledFeatures(KEYGUARD_DISABLE_TRUST_AGENTS)`](http://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setKeyguardDisabledFeatures%28android.content.ComponentName,%20int%29)
         method or the [`DevicePolicyManager.setPasswordQuality()`](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordQuality%28android.content.ComponentName,%20int%29)
         method with a more restrictive quality constant than
         `PASSWORD_QUALITY_UNSPECIFIED`.
*    If based on biometrics, MUST meet all following requirements:
     *    It MUST have a fall-back mechanism to use one of the primary
          authentication methods which is based on a known secret and meets
          the requirements to be treated as a secure lock screen.
     *    It MUST be disabled and only allow the primary authentication to
          unlock the screen when the Device Policy Controller (DPC) application
          has set the keguard feature policy by calling the method
          [`DevicePolicyManager.setKeyguardDisabledFeatures(KEYGUARD_DISABLE_FINGERPRINT)`](http://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setKeyguardDisabledFeatures%28android.content.ComponentName,%20int%29).
     *    It MUST have a false acceptance rate that is equal or stronger than
          what is required for a fingerprint sensor as described in
          section 7.3.10, or otherwise MUST be disabled and only allow the
          primary authentication to unlock the screen when the Device Policy
          Controller (DPC) application has set the password quality policy
          via the [`DevicePolicyManager.setPasswordQuality()`](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html\#setPasswordQuality%28android.content.ComponentName,%20int%29)
          method with a more restrictive quality constant than
          `PASSWORD_QUALITY_BIOMETRIC_WEAK`.

If such an authentication method will be used to unlock the keyguard, but will
not be treated as a secure lock screen, it:

*    MUST return `false` for both the [`KeyguardManager.isKeyguardSecure()`](http://developer.android.com/reference/android/app/KeyguardManager.html#isKeyguardSecure%28%29)
     and the [`KeyguardManager.isDeviceSecure()`](https://developer.android.com/reference/android/app/KeyguardManager.html#isDeviceSecure%28%29)
     methods.
*    MUST be disabled when the Device Policy Controller (DPC) application
     has set the password quality policy via the [`DevicePolicyManager.setPasswordQuality()`](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordQuality%28android.content.ComponentName,%20int%29)
     method with a more restrictive quality constant than `PASSWORD_QUALITY_UNSPECIFIED`.
*    MUST NOT reset the password expiration timers set by [`DevicePolicyManager.setPasswordExpirationTimeout()`](http://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordExpirationTimeout%28android.content.ComponentName,%20long%29).
*    MUST NOT authenticate access to keystores if the application has called
     [`KeyGenParameterSpec.Builder.setUserAuthenticationRequired(true)`](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.Builder.html#setUserAuthenticationRequired%28boolean%29)).

