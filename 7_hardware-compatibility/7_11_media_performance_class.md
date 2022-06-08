### 7.11\. Media Performance Class

The media performance class of the device implementation can be obtained from
the `android.os.Build.VERSION_CODES.MEDIA_PERFORMANCE_CLASS` API. Requirements
for media performance class are defined for each Android version starting with
R (version 30). The special value of 0 designates that the device is not of a
media performance class.

If device implementations return non-zero value for
`android.os.Build.VERSION_CODES.MEDIA_PERFORMANCE_CLASS`, they:

*   [C-1-1] MUST return at least a value of `android.os.Build.VERSION_CODES.R`.

*   [C-1-2] MUST be a handheld device implementation.

*   [C-1-3] MUST meet all requirements for "Media Performance Class" described
    in [section 2.2.7](#227_handheld_media_performance_class).

See [section 2.2.7](#227_handheld_media_performance_class) for device-specific
requirements.