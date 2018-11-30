## 9.11\. Keys and Credentials

The [Android Keystore System](https://developer.android.com/training/articles/keystore.html)
allows app developers to store cryptographic keys in a container and use them in
cryptographic operations through the [KeyChain API](https://developer.android.com/reference/android/security/KeyChain.html)
or the [Keystore API](https://developer.android.com/reference/java/security/KeyStore.html).
Device implementations:

*    [C-0-1] MUST allow at least 8,192 keys to be imported or generated.
*    [C-0-2] The lock screen authentication MUST rate-limit attempts and MUST
have an exponential backoff algorithm. Beyond 150 failed attempts, the delay
MUST be at least 24 hours per attempt.
*    SHOULD not limit the number of keys that can be generated

When the device implementation supports a secure lock screen, it:

*    [C-1-1] MUST back up the keystore implementation with an isolated
     execution environment.
*    [C-1-2] MUST have implementations of RSA, AES, ECDSA and HMAC cryptographic
algorithms and MD5, SHA1, and SHA-2 family hash functions to properly support
the Android Keystore system's supported algorithms in an area that is securely
isolated from the code running on the kernel and above. Secure isolation MUST
block all potential mechanisms by which kernel or userspace code might access
the internal state of the isolated environment, including DMA. The upstream
Android Open Source Project (AOSP) meets this requirement by using the
[Trusty](https://source.android.com/security/trusty/) implementation, but
another ARM TrustZone-based solution or a third-party reviewed secure
implementation of a proper hypervisor-based isolation are alternative options.
*    [C-1-3] MUST perform the lock screen authentication in the isolated
execution environment and only when successful, allow the authentication-bound
keys to be used. Lock screen credentials MUST be stored in a
way that allows only the isolated execution environment to perform lock screen
authentication. The upstream Android Open Source Project provides the
[Gatekeeper Hardware Abstraction Layer (HAL)](http://source.android.com/devices/tech/security/authentication/gatekeeper.html)
and Trusty, which can be used to satisfy this requirement.
*    [C-1-4] MUST support key attestation where the attestation signing key is
protected by secure hardware and signing is performed in secure hardware. The
attestation signing keys MUST be shared across large enough number of devices to
prevent the keys from being used as device identifiers. One way of meeting this
requirement is to share the same attestation key unless at least 100,000 units
of a given SKU are produced. If more than 100,000 units of an SKU are produced,
a different key MAY be used for each 100,000 units.
*    [C-1-5] MUST allow the user to choose the Sleep timeout for transition from
     the unlocked to the locked state, with a minimum allowable timout up to
     15 seconds.

Note that if a device implementation is already launched on an earlier Android
version, such a device is exempted from the requirement to have a keystore
backed by an isolated execution environment and support the key attestation,
unless it declares the `android.hardware.fingerprint` feature which requires a
keystore backed by an isolated execution environment.

### 9.11.1\. Secure Lock Screen

The AOSP implementation follows a tiered authentication model where a
knowledge-factory based primary authentication can be backed by either a
secondary strong biometric, or by weaker tertiary modalities.

Device implementations:

*    [C-SR] Are STRONGLY RECOMMENDED to set only one of the following as the primary authentication
method:
     *     A numerical PIN,
     *     An alphanumerical password, or
     *     A swipe pattern on a grid of exactly 3x3 dots.

Note that the above authentication methods are referred as the recommended
primary authentication methods in this document.

If device implementations add or modify the recommended primary authentication
methods and use a new authentication method as a secure way to lock the screen,
the new authentication method:

*    [C-2-1] MUST be the user authentication method as described in
     [Requiring User Authentication For Key Use](
     https://developer.android.com/training/articles/keystore.html#UserAuthentication).
*    [C-2-2] MUST unlock all keys for a third-party developer app to use when
     the user unlocks the secure lock screen. For example, all keys MUST be
     available for a third-party developer app through relevant APIs, such as
     [`createConfirmDeviceCredentialIntent`](
     https://developer.android.com/reference/android/app/KeyguardManager.html#createConfirmDeviceCredentialIntent%28java.lang.CharSequence, java.lang.CharSequence%29)
     and [`setUserAuthenticationRequired`](
     https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.Builder.html#setUserAuthenticationRequired%28boolean%29).

If device implementations add or modify the authentication methods to unlock
the lock screen if based on a known secret and use a new authentication
method to be treated as a secure way to lock the screen:

*    [C-3-1] The entropy of the shortest allowed length of inputs MUST be
     greater than 10 bits.
*    [C-3-2] The maximum entropy of all possible inputs MUST be greater than
     18 bits.
*    [C-3-3] The new authentication method MUST NOT replace any of the
     recommended primary authentication methods (i.e. PIN, pattern, password)
     implemented and provided in AOSP.
*    [C-3-4] The new authentication method MUST be disabled when the Device
     Policy Controller (DPC) application has set the password quality policy
     via the
     [`DevicePolicyManager.setPasswordQuality()`](
     https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordQuality%28android.content.ComponentName,%20int%29)
     method with a more restrictive quality constant than
    `PASSWORD_QUALITY_SOMETHING`.

If device implementations add or modify the recommended primary authentication
methods to unlock the lock screen and use a new authentication method that is
based on biometrics to be treated as a secure way to lock the screen, the new
method:

*    [C-4-1] MUST meet all requirements described in
     [section 7.3.10.2](#7_3_10_2_other_biometric_sensors).
*    [C-4-2] MUST have a fall-back mechanism to use one of the recommended
     primary authentication methods which is based on a known secret.
*    [C-4-3] MUST be disabled and only allow the recommended primary
     authentication to unlock the screen when the Device Policy Controller (DPC)
     application has set the keguard feature policy by calling the method
     [`DevicePolicyManager.setKeyguardDisabledFeatures()`](
     http://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setKeyguardDisabledFeatures%28android.content.ComponentName,%20int%29)
     , with any of the associated biometric flags (i.e.
     `KEYGUARD_DISABLE_BIOMETRICS`, `KEYGUARD_DISABLE_FINGERPRINT`,
     `KEYGUARD_DISABLE_FACE`, or `KEYGUARD_DISABLE_IRIS`).
*    [C-4-4] MUST challenge the user for the recommended primary authentication
     (e.g. PIN, pattern, password) at least once very 72 hours or less.
*    [C-4-5] MUST have a false acceptance rate that is equal or stronger than
     what is required for a fingerprint sensor as described in section
     [section 7.3.10](#7_3_10_biometric_sensors),
     or otherwise
     MUST be disabled and only allow the recommended primary authentication
     to unlock the screen when the Device Policy Controller (DPC) application
     has set the password quality policy via the
    [`DevicePolicyManager.setPasswordQuality()`](
    https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html\#setPasswordQuality%28android.content.ComponentName,%20int%29)
    method with a more restrictive quality constant than
   `PASSWORD_QUALITY_BIOMETRIC_WEAK`.
*    [C-SR] Are STRONGLY RECOMMENDED to have spoof and imposter acceptance rates
     that are equal to or stronger than what is required for a fingerprint
     sensor as described in [section 7.3.10](#7_3_10_biometric_sensors).
*    [C-4-6] MUST have a secure processing pipeline such that an operating
     system or kernel compromise cannot allow data to be directly injected to
     falsely authenticate as the user.
*    [C-4-7] MUST be paired with an explicit confirm action (eg: a button press)
     to allow access to keystore keys if the application sets `true` for
     [`KeyGenParameterSpec.Built.setUserAuthenticationRequired()`](
     https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.Builder.html#setUserAuthenticationRequired%28boolean%29)
     and the biometric is passive (e.g. face or iris where no explicit
     signal of intent exists).
*    [C-SR] The confirm action for passive biometrics is STRONGLY RECOMMENDED to
     be secured such that an operating system or kernel compromise cannot spoof
     it. For example, this means that the confirm action based on a physical
     button is routed through an input-only general-purpose input/output (GPIO)
     pin of a secure element (SE) that cannot be driven by any other means
     than a physical button press.

If the biometric authentication methods do not meet the spoof and imposter
acceptance rates as described in [section 7.3.10](#7_3_10_biometric_sensors):

*    [C-5-1] The methods MUST be disabled if the Device Policy Controller (DPC)
     application has set the password quality policy via the [`DevicePolicyManager.setPasswordQuality()`](
     https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html\#setPasswordQuality%28android.content.ComponentName,%20int%29)
     method with a more restrictive quality constant than
     `PASSWORD_QUALITY_BIOMETRIC_WEAK`.
*    [C-5-2] The user MUST be challenged for the recommended primary
     authentication (eg: PIN, pattern, password) after any 4-hour idle timeout
     period. The idle timeout period is reset after any successful confirmation
     of the device credentials.
*    [C-5-3] The methods MUST NOT be treated as a secure lock screen, and MUST
     meet the requirements that start with C-8 in this section below.

If device implementations add or modify the authentication methods to unlock
the lock screen and a new authentication method is based on a physical token
or the location:

*    [C-6-1] They MUST have a fall-back mechanism to use one of the recommended
     primary authentication methods which is based on a known secret and meet
     the requirements to be treated as a secure lock screen.
*    [C-6-2] The new method MUST be disabled and only allow one of the
     recommended primary authentication methods to unlock the screen when the
     Device Policy Controller (DPC) application has set the policy with either
     the
     [`DevicePolicyManager.setKeyguardDisabledFeatures(KEYGUARD_DISABLE_TRUST_AGENTS)`](
     http://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setKeyguardDisabledFeatures%28android.content.ComponentName,%20int%29)
     method or the
     [`DevicePolicyManager.setPasswordQuality()`](
     https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordQuality%28android.content.ComponentName,%20int%29)
     method with a more restrictive quality constant than
     `PASSWORD_QUALITY_UNSPECIFIED`.
*    [C-6-3] The user MUST be challenged for one of the recommended primary
     authentication methods (e.g.PIN, pattern, password) at least once every 72
     hours or less.
*    [C-6-4] The new method MUST NOT be treated as a secure lock screen and MUST
     follow the constraints listed in C-8 below.

If device implementations have a secure lock screen and include one or more
trust agent, which implements the `TrustAgentService` System API, they:

*    [C-7-1] MUST have clear indication in the settings menu and on the lock
     screen when device lock is deferred or can be unlocked by trust agent(s).
     For example, AOSP meets this requirement by showing a text description for
     the "Automatically lock setting" and "Power button instantly locks" in the
     settings menu and a distinguishable icon on the lock screen.
*    [C-7-2] MUST respect and fully implement all trust agent APIs in the
     `DevicePolicyManager` class, such as the
     [`KEYGUARD_DISABLE_TRUST_AGENTS`](
     https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#KEYGUARD&lowbarDISABLE&lowbarTRUST&lowbarAGENTS)
     constant.
*    [C-7-3] MUST NOT fully implement the `TrustAgentService.addEscrowToken()`
     function on a device that is used as a primary personal device
     (e.g. handheld) but MAY fully implement the function on device
     implementations that are typically shared (e.g. Android Television or
     Automotive device).
*    [C-7-4] MUST encrypt all stored tokens added by
     `TrustAgentService.addEscrowToken()`.
*    [C-7-5] MUST NOT store the encryption key on the same device where the key
     is used. For example, it is allowed for a key stored on a phone to unlock a
     user account on a TV.
*    [C-7-6] MUST inform the user about the security implications before
     enabling the escrow token to decrypt the data storage.
*    [C-7-7] MUST have a fall-back mechanism to use one of the recommended
     primary authentication methods.
*    [C-7-8] The user MUST be challenged for one of the recommended primary
     authentication (eg: PIN, pattern, password) methods at least once every 72
     hours or less.
*    [C-7-9] The user MUST be challenged for one of the recommended primary
     authentication (eg: PIN, pattern, password) methods after any 4-hour idle
     timeout period. The idle timeout period is reset after any successful
     confirmation of the device credentials.
*    [C-7-10] MUST NOT be treated as a secure lock screen and MUST follow the
     constraints listed in C-8 below.

If device implementations add or modify the authentication methods to unlock
the lock screen that is not a secure lock screen as described above, and use
a new authentication method to unlock the keyguard:

*    [C-8-1] The new method MUST be disabled when the Device Policy Controller
     (DPC) application has set the password quality policy via the
     [`DevicePolicyManager.setPasswordQuality()`](
     https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordQuality%28android.content.ComponentName,%20int%29)
     method with a more restrictive quality constant than
     `PASSWORD_QUALITY_UNSPECIFIED`.
*    [C-8-2] They MUST NOT reset the password expiration timers set by
     [`DevicePolicyManager.setPasswordExpirationTimeout()`](
     http://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setPasswordExpirationTimeout%28android.content.ComponentName,%20long%29).
*    [C-8-3] They MUST NOT authenticate access to keystores when the application
     sets `true` for
     [`KeyGenParameterSpec.Builder.setUserAuthenticationRequired()`](
     https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.Builder.html#setUserAuthenticationRequired%28boolean%29)).

### 9.11.2\. StrongBox

The [Android Keystore System](
https://developer.android.com/training/articles/keystore.html) allows
app developers to store cryptographic keys in a dedicated secure processor as
well as the isolated execution environment described above.

Device implementations:

*    [C-SR] Are STRONGLY RECOMMENDED to support StrongBox.

If device implementations support StrongBox, they:

*    [C-1-1] MUST declare [FEATURE_STRONGBOX_KEYSTORE](
https://developer.android.com/reference/kotlin/android/content/pm/PackageManager#FEATURE_STRONGBOX_KEYSTORE%3Akotlin.String).

*    [C-1-2] MUST provide dedicated secure hardware that is used to back
keystore and secure user authentication.

*    [C-1-3] MUST have a discrete CPU that shares no cache, DRAM, coprocessors
or other core resources with the application processor (AP).

*    [C-1-4] MUST ensure that any peripherals shared with the AP cannot alter
StrongBox processing in any way, or obtain any information from the StrongBox.
The AP MAY disable or block access to StrongBox.

*    [C-1-5] MUST have an internal clock with reasonable accuracy (+-10%)
that is immune to manipulation by the AP.

*    [C-1-6] MUST have a true random number generator that produces
uniformly-distributed and unpredictable output.

*    [C-1-7] MUST have tamper resistance, including resistance against
physical penetration, and glitching.

*    [C-1-8] MUST have side-channel resistance, including resistance against
leaking information via power, timing, electromagnetic radiation, and thermal
radiation side channels.

*    [C-1-9] MUST have secure storage which ensures confidentiality,
integrity, authenticity, consistency, and freshness of the
contents. The storage MUST NOT be able to be read or altered, except
as permitted by the StrongBox APIs.

*    To validate compliance with [C-1-3] through [C-1-9], device
     implementations:

    *    [C-1-10] MUST include the hardware that is certified against the
         Secure IC Protection Profile [BSI-CC-PP-0084-2014](
         https://www.commoncriteriaportal.org/files/ppfiles/pp0084b_pdf.pdf) or
         evaluated by a nationally accredited testing laboratory incorporating
         High attack potential vulnerability assessment according to the
         [Common Criteria Application of Attack Potential to Smartcards](
       https://www.commoncriteriaportal.org/files/supdocs/CCDB-2013-05-002.pdf).
    *    [C-1-11] MUST include the firmware that is evaluated by a
         nationally accredited testing laboratory incorporating High attack
         potential vulnerability assessment according to the
         [Common Criteria Application of Attack Potential to Smartcards](
         https://www.commoncriteriaportal.org/files/supdocs/CCDB-2013-05-002.pdf).
    *    [C-SR] Are STRONGLY RECOMMENDED to include the hardware that is
         evaluated using a Security Target, Evaluation Assurance Level
         (EAL) 5, augmented by AVA_VAN.5.  EAL 5 certification will likely
         become a requirement in a future release.

*    [C-SR] are STRONGLY RECOMMENDED to provide insider attack resistance (IAR),
which means that an insider with access to firmware signing keys cannot produce
firmware that causes the StrongBox to leak secrets, to bypass functional
security requirements or otherwise enable access to sensitive user data. The
recommended way to implement IAR is to allow firmware updates only when the
primary user password is provided via the IAuthSecret HAL. IAR will likely
become a requirement in a future release.