## 9.9\. Data Storage Encryption

Device implementations:

*   [C-0-1] MUST support data storage encryption of the application private
data (`/data partition`), as well as the application shared storage partition
(`/sdcard partition`) if it is a permanent, non-removable part of the device.

If device implementations are already launched on an earlier Android version
without data storage encryption described above, such a device MAY be exempted.

If device implementations support a secure lock screen as described in
[section 9.11.1](#9_11_1_secure_lock_screen), they:

*    [C-2-1] MUST enable the data storage encryption by default at the time
the user has completed the out-of-box setup experience. If device
implementations are already launched on an earlier Android version with
encryption disabled by default, such a device cannot meet the requirement
through a system software update and thus MAY be exempted.

*    SHOULD meet the above data storage encryption
requirement via implementing [File Based Encryption](
https://source.android.com/security/encryption/file-based.html) (FBE).

### 9.9.1\. Direct Boot

Device implementations:

*    [C-0-1] MUST implement the [Direct Boot mode](
http://developer.android.com/preview/features/direct-boot.html) APIs even if
they do not support Storage Encryption.

*     [C-0-2] The [`ACTION_LOCKED_BOOT_COMPLETED`](
https://developer.android.com/reference/android/content/Intent.html#ACTION_LOCKED_BOOT_COMPLETED)
and [`ACTION_USER_UNLOCKED`](https://developer.android.com/reference/android/content/Intent.html#ACTION_USER_UNLOCKED)
Intents MUST still be broadcast to signal Direct Boot aware applications that
Device Encrypted (DE) and Credential Encrypted (CE) storage locations are
available for user.

### 9.9.2\. File Based Encryption

If device implementations support FBE, they:

*    [C-1-1] MUST boot up without challenging the user for credentials and
allow Direct Boot aware apps to access to the Device Encrypted (DE) storage
after the `ACTION_LOCKED_BOOT_COMPLETED` message is broadcasted.
*    [C-1-2] MUST only allow access to Credential Encrypted (CE) storage after
the user has unlocked the device by supplying their credentials
(eg. passcode, pin, pattern or fingerprint) and the `ACTION_USER_UNLOCKED`
message is broadcasted.
*    [C-1-3] MUST NOT offer any method to unlock the CE protected storage
without either the user-supplied credentials or a registered escrow key.
*    [C-1-4] MUST support Verified Boot and ensure that DE keys are
cryptographically bound to the device's hardware root of trust.
*    [C-1-5] MUST support encrypting file contents using AES-256-XTS or
Speck128/256-XTS. AES-256-XTS refers to the Advanced Encryption Standard with
a 256-bit key length, operated in XTS mode.  Speck128/256-XTS refers to the
[Speck block cipher](https://eprint.iacr.org/2013/404) with a 128-bit block
length and 256-bit key length, operated in XTS mode.  In both cases, the full
length of the XTS key is 512 bits.
*    [C-1-6] MUST support encrypting file names using AES-256 or Speck128/256,
in CBC-CTS mode.
*    [C-1-7] MUST use AES rather than Speck128 for both file contents and file
names if AES-256-XTS encryption or decryption performance is at least
50 MiB/s.  Measured AES speeds MUST take advantage of AES instructions (e.g.
the ARM Cryptography Extensions) if supported by the CPU and they result in
a faster speed than other AES implementations.

*   The keys protecting CE and DE storage areas:

   *   [C-1-7] MUST be cryptographically bound to a hardware-backed Keystore.
   *   [C-1-8] CE keys MUST be bound to a user's lock screen credentials.
   *   [C-1-9] CE keys MUST be bound to a default passcode when the user has
not specified lock screen credentials.
   *   [C-1-10] MUST be unique and distinct, in other words no user's CE or DE
   key matches any other user's CE or DE keys.

   *    [C-1-11] MUST use the mandatorily supported ciphers, key lengths and
   modes by default.

*    SHOULD make preloaded essential apps (e.g. Alarm, Phone, Messenger)
Direct Boot aware.
*    MAY support alternative ciphers, key lengths and modes for file content
and file name encryption.

The upstream Android Open Source project provides a preferred implementation of
this feature based on the Linux kernel ext4 encryption feature.

### 9.9.3\. Full Disk Encryption

If device implementations support [full disk encryption](
http://source.android.com/devices/tech/security/encryption/index.html)
(FDE), they:

*   [C-1-1] MUST use AES or Speck128 in a mode designed for storage (for
example, XTS or CBC-ESSIV), and with a cipher key length of 128 bits or greater.
*   [C-1-3] MUST use AES rather than Speck128 if AES-XTS or AES-CBC encryption
or decryption performance is at least 50 MiB/s.  Measured AES speeds
MUST take advantage of AES instructions (e.g. the ARM Cryptography Extensions)
if supported by the CPU and if using these instructions results in a faster speed
than other AES implementations.
*   [C-1-2] MUST use a default passcode to wrap the encryption key and
MUST NOT write the encryption key to storage at any time
without being encrypted.
   *   [C-1-6] MUST AES encrypt the encryption key by default unless the user
   explicitly opts out, except when it is in active use, with the lock screen
   credentials stretched using a slow stretching algorithm
   (e.g. PBKDF2 or scrypt).
*   [C-1-4] The above default password stretching algorithm MUST be
cryptographically bound to that keystore when the user has not specified a lock
screen credentials or has disabled use of the passcode for encryption and
the device provides a hardware-backed keystore.
*   [C-1-5] MUST NOT send encryption key off the device
(even when wrapped with the user passcode and/or hardware bound key).

The upstream Android Open Source project provides a preferred implementation
of this feature, based on the Linux kernel feature dm-crypt.
