## 3.11\. Text-to-Speech

Android includes APIs that allow applications to make use of text-to-speech
(TTS) services and allows service providers to provide implementations of TTS
services.

If device implementations reporting the feature android.hardware.audio.output,
they:

*   [C-1-1] MUST support the [Android TTS framework](
http://developer.android.com/reference/android/speech/tts/package-summary.html)
APIs.

If device implementations support installation of third-party TTS engines, they:

*   [C-2-1] MUST provide user affordance to allow the user to select a TTS
    engine for use at system level.

*   [H-0-1] STRONGLY RECOMMENDED to include a TTS engine supporting the
    languages available on the device.
*   [W-0-1] STRONGLY RECOMMENDED to include a TTS engine supporting the
    languages available on the device.
*   [T-0-1] STRONGLY RECOMMENDED to include a TTS engine supporting the
    languages available on the device.

*   [H-0-2] MUST support installation of third-party TTS engines.
*   [W-0-2] MUST support installation of third-party TTS engines.
*   [T-0-2] MUST support installation of third-party TTS engines.