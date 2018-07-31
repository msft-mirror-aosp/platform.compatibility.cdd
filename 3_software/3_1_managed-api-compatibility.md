## 3.1\. Managed API Compatibility

The managed Dalvik bytecode execution environment is the primary vehicle for
Android applications. The Android application programming interface (API) is the
set of Android platform interfaces exposed to applications running in the
managed runtime environment.

Device implementations:

*    [C-0-1] MUST provide complete implementations,
including all documented behaviors, of any documented API exposed by the
[Android SDK](http://developer.android.com/reference/packages.html)
or any API decorated with the “@SystemApi” marker in the upstream Android
source code.

*    [C-0-2] MUST support/preserve all classes,
methods, and associated elements marked by the TestApi annotation (@TestApi).

*    [C-0-3] MUST NOT omit any managed APIs, alter
API interfaces or signatures, deviate from the documented behavior, or include
no-ops, except where specifically allowed by this Compatibility Definition.

*    [C-0-4] MUST still keep the APIs present and behave
     in a reasonable way, even when some hardware features for which Android
     includes APIs are omitted. See [section 7](#7_hardware_compatibility)
     for specific requirements for this scenario.

*    [C-0-5] MUST display a warning to the user that an app was built for an
     older version of Android when the app targeting API level 16 or lower is
     first launched.

## 3.1.1\. Android Extensions

Android includes the support of extending the managed APIs while keeping the
same API level version.

*   [C-0-1] Android device implementations MUST preload the AOSP implementation
of both the shared library `ExtShared` and services `ExtServices` with versions
higher than or equal to the minimum versions allowed per each API level.
For example, Android 7.0 device implementations, running API level 24 MUST
include at least version 1.

## 3.1.2\. Android Library

Due to [Apache HTTP client deprecation](https://developer.android.com/preview/behavior-changes#apache-p),
device implementations:

*   [C-0-1] MUST NOT place the `org.apache.http.legacy` library in the
bootclasspath.
*   [C-0-2] MUST add the `org.apache.http.legacy` library to the application
classpath only when the app satisfies one of the following conditions:
    *    Targets API level 28 or lower.
    *    Declares in its manifest that it needs the library by setting the
    `android:name` attribute of `<uses-library>` to `org.apache.http.legacy`.

The AOSP implementation meets these requirements.