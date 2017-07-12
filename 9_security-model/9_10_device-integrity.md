## 9.10\. Device Integrity

The following requirements ensures there is transparancy to the status of the
device integrity.

Device implementations MUST correctly report through the System API method
PersistentDataBlockManager.getFlashLockState() whether their bootloader state
permits flashing of the system image. The `FLASH_LOCK_UNKNOWN` state is reserved
for device implementations upgrading from an earlier version of Android where this
new system API method did not exist.

Verified boot is a feature that guarantees the integrity of the device
software. If a device implementation supports the feature, it:

*   MUST declare the platform feature flag `android.software.verified_boot`.
*   MUST perform verification on every boot sequence.
*   MUST start verification from an immutable hardware key that is the root of trust
    and go all the way up to the system partition.
*   MUST implement each stage of verification to check the integrity and
    authenticity of all the bytes in the next stage before executing the code in
    the next stage.
*   MUST use verification algorithms as strong as current recommendations from NIST
    for hashing algorithms (SHA-256) and public key sizes (RSA-2048).
*   MUST NOT allow boot to complete when system verification fails, unless the
    user consents to attempt booting anyway, in which case the data from any
    non-verified storage blocks MUST not be used.
*   MUST NOT allow verified partitions on the device to be modified unless the
    user has explicitly unlocked the boot loader.
*   If there are multiple discrete chips in the device (e.g. radio, specialized image
    processor), the boot process of each of those chips is STRONGLY RECOMMENDED to
    verify every stage upon booting.
*   STRONGLY RECOMMENDED to use tamper-evident storage: for when the boot loader
    is unlocked.
    *   Tamper-evident storage means that the boot loader can detect if the storage has been
        tampered with from inside the HLOS (High Level Operating System).
*   STRONGLY RECOMMENDED to prompt the user, while using the device, and require
    physical confirmation before allowing a transition from boot loader locked
    mode to boot loader unlocked mode.
*   STRONGLY RECOMMENDED to implement rollback protection for the HLOS
    (e.g. boot, system partitions) and to use tamper-evident storage for storing the
    metadata used for determining the minimum allowable OS version.
*   SHOULD implement rollback protection for any component with persistent
    firmware (e.g. modem, camera) and SHOULD use tamper-evident storage for
    storing the metadata used for determining the minimum allowable version.

The upstream Android Open Source Project provides a preferred implementation of
this feature in the [`external/avb/`](http://android.googlesource.com/platform/external/avb/)
repository, which can be integrated into the boot loader used for loading Android.

Starting from Android 6.0, device implementations with Advanced Encryption
Standard (AES) crypto performance above 50 MiB/seconds MUST support verified boot
for device integrity.

If a device implementation is already launched without supporting verified boot
on an earlier version of Android, such a device can not add support for this feature
with a system software update and thus are exempted from the requirement.

