## 5.3\. Video Decoding

If device implementations support VP8, VP9, H.264, or H.265 codecs, they:

*   [C-1-1] MUST support dynamic video resolution and frame rate switching
through the standard Android APIs within the same stream for all VP8, VP9,
H.264, and H.265 codecs in real time and up to the maximum resolution supported
by each codec on the device.

### 5.3.1\. MPEG-2

If device implementations support MPEG-2 decoders, they:

*   [C-1-1] MUST support the Main Profile High Level.

### 5.3.2\. H.263

If device implementations support H.263 decoders, they:

*   [C-1-1] MUST support Baseline Profile Level 30 and Level 45.

### 5.3.3\. MPEG-4

If device implementations with MPEG-4 decoders, they:

*   [C-1-1] MUST support Simple Profile Level 3.

### 5.3.4\. H.264

If device implementations support H.264 decoders, they:

*   [C-1-1] MUST support Main Profile Level 3.1 and Baseline Profile. Support
for ASO (Arbitrary Slice Ordering), FMO (Flexible Macroblock Ordering) and RS
(Redundant Slices) is OPTIONAL.
*   [C-1-2] MUST be capable of decoding videos with the SD (Standard Definition)
    profiles listed in the following table and encoded with the Baseline Profile
    and Main Profile Level 3.1 (including 720p30).
*   SHOULD be capable of decoding videos with the HD (High Definition) profiles
    as indicated in the following table.

If the height that is reported by the `Display.getSupportedModes()` method is
equal or greater than the video resolution, device implementations:

*   [C-2-1] MUST support the HD 720p video decoding profiles in the following
table.
*   [C-2-2] MUST support the HD 1080p video decoding profiles in the following
table.


<table>
 <tr>
    <th></th>
    <th>SD (Low quality)</th>
    <th>SD (High quality)</th>
    <th>HD 720p</th>
    <th>HD 1080p</th>
 </tr>
 <tr>
    <th>Video resolution</th>
    <td>320 x 240 px</td>
    <td>720 x 480 px</td>
    <td>1280 x 720 px</td>
    <td>1920 x 1080 px</td>
 </tr>
 <tr>
    <th>Video frame rate</th>
    <td>30 fps</td>
    <td>30 fps</td>
    <td>60 fps</td>
    <td>30 fps (60 fps<sup>Television</sup>)</td>
 </tr>
 <tr>
    <th>Video bitrate</th>
    <td>800 Kbps </td>
    <td>2 Mbps</td>
    <td>8 Mbps</td>
    <td>20 Mbps</td>
 </tr>
</table>

### 5.3.5\. H.265 (HEVC)


If device implementations support H.265 codec, they:

*   [C-1-1] MUST support the Main Profile Level 3 Main tier and the SD video
decoding profiles as indicated in the following table.
*   SHOULD support the HD decoding profiles as indicated in the following table.
*   [C-1-2] MUST support the HD decoding profiles as indicated in the following
table if there is a hardware decoder.

If the height that is reported by the `Display.getSupportedModes()` method is
equal to or greater than the video resolution, then:

*   [C-2-1] Device implementations MUST support at least one of H.265 or VP9
decoding of 720, 1080 and UHD profiles.

<table>
 <tr>
    <th></th>
    <th>SD (Low quality)</th>
    <th>SD (High quality)</th>
    <th>HD 720p</th>
    <th>HD 1080p</th>
    <th>UHD</th>
 </tr>
 <tr>
    <th>Video resolution</th>
    <td>352 x 288 px</td>
    <td>720 x 480 px</td>
    <td>1280 x 720 px</td>
    <td>1920 x 1080 px</td>
    <td>3840 x 2160 px</td>
 </tr>
 <tr>
    <th>Video frame rate</th>
    <td>30 fps</td>
    <td>30 fps</td>
    <td>30 fps</td>
    <td>30/60 fps (60 fps<sup>Television with H.265 hardware decoding</sup>)</td>
    <td>60 fps</td>
 </tr>
 <tr>
    <th>Video bitrate</th>
    <td>600 Kbps </td>
    <td>1.6 Mbps</td>
    <td>4 Mbps</td>
    <td>5 Mbps</td>
    <td>20 Mbps</td>
 </tr>
</table>

If device implementations claim to support an HDR Profile
(`HEVCProfileMain10HDR10`, `HEVCProfileMain10HDR10Plus`) through the Media APIs:

*   [C-3-1] Device implementations MUST accept the required HDR metadata
    ([MediaFormat#KEY_HDR_STATIC_INFO](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR_STATIC_INFO)
    for all HDR profiles) from the application using MediaCodec API, as well as
    support extracting the required HDR metadata
    ([MediaFormat#KEY_HDR_STATIC_INFO](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR_STATIC_INFO)
    for all HDR profiles, as well as
    [MediaFormat#KEY_HDR10_PLUS_INFO](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR10_PLUS_INFO)
    for HDR10Plus profiles) from the bitstream and/or container as defined by
    the relevant specifications. They MUST also support outputting the required
    HDR metadata ([MediaFormat#KEY_HDR_STATIC_INFO](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR_STATIC_INFO)
    for all HDR profiles) from the bitstream and/or container as defined by the
    relevant specifications.

*   [C-SR] The device implementations are STRONGLY RECOMMENDED to support
    outputting the metadata [MediaFormat#KEY_HDR10_PLUS_INFO](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR10_PLUS_INFO)
    for HDR10Plus profiles via
    [MediaCodec#getOutputFormat(int)](
    https://developer.android.com/reference/android/media/MediaCodec#getOutputFormat%28int%29)`.`

*   [C-3-2] Device implementations MUST properly display HDR content for
    `HEVCProfileMain10HDR10` profile on the device screen or on a standard video
    output port (e.g., HDMI).

*   [C-SR] Device implementations are STRONGLY RECOMMENDED to properly display
    HDR content for `HEVCProfileMain10HDR10Plus` profile on the device screen or
    on a standard video output port (e.g., HDMI).

### 5.3.6\. VP8

If device implementations support VP8 codec, they:

*   [C-1-1] MUST support the SD decoding profiles in the following table.
*   SHOULD use a hardware VP8 codec that meets the
[requirements]("http://www.webmproject.org/hardware/rtc-coding-requirements/").
*   SHOULD support the HD decoding profiles in the following table.


If the height as reported by the `Display.getSupportedModes()` method is equal
or greater than the video resolution, then:

*   [C-2-1] Device implementations MUST support 720p profiles in the
following table.
*   [C-2-2] Device implementations MUST support 1080p profiles in the
following table.


<table>
 <tr>
    <th></th>
    <th>SD (Low quality)</th>
    <th>SD (High quality)</th>
    <th>HD 720p</th>
    <th>HD 1080p</th>
 </tr>
 <tr>
    <th>Video resolution</th>
    <td>320 x 180 px</td>
    <td>640 x 360 px</td>
    <td>1280 x 720 px</td>
    <td>1920 x 1080 px</td>
 </tr>
 <tr>
    <th>Video frame rate</th>
    <td>30 fps</td>
    <td>30 fps</td>
    <td>30 fps (60 fps<sup>Television</sup>)</td>
    <td>30 (60 fps<sup>Television</sup>)</td>
 </tr>
 <tr>
    <th>Video bitrate</th>
    <td>800 Kbps </td>
    <td>2 Mbps</td>
    <td>8 Mbps</td>
    <td>20 Mbps</td>
 </tr>
</table>


### 5.3.7\. VP9

If device implementations support VP9 codec, they:

*   [C-1-1] MUST support the SD video decoding profiles as indicated in the
following table.
*   SHOULD support the HD decoding profiles as indicated in the following table.

If device implementations support VP9 codec and a hardware decoder:

*   [C-2-1] MUST support the HD decoding profiles as indicated in the following
table.

If the height that is reported by the `Display.getSupportedModes()` method is
equal to or greater than the video resolution, then:

*   [C-3-1] Device implementations MUST support at least one of VP9 or H.265
decoding of the 720, 1080 and UHD profiles.

<table>
 <tr>
    <th></th>
    <th>SD (Low quality)</th>
    <th>SD (High quality)</th>
    <th>HD 720p</th>
    <th>HD 1080p</th>
    <th>UHD</th>
 </tr>
 <tr>
    <th>Video resolution</th>
    <td>320 x 180 px</td>
    <td>640 x 360 px</td>
    <td>1280 x 720 px</td>
    <td>1920 x 1080 px</td>
    <td>3840 x 2160 px</td>
 </tr>
 <tr>
    <th>Video frame rate</th>
    <td>30 fps</td>
    <td>30 fps</td>
    <td>30 fps</td>
    <td>30 fps (60 fps<sup>Television with VP9 hardware decoding</sup>)</td>
    <td>60 fps</td>
 </tr>
 <tr>
    <th>Video bitrate</th>
    <td>600 Kbps</td>
    <td>1.6 Mbps</td>
    <td>4 Mbps</td>
    <td>5 Mbps</td>
    <td>20 Mbps</td>
 </tr>
</table>

If device implementations claim to support `VP9Profile2` or `VP9Profile3`
through the ['CodecProfileLevel'](
https://developer.android.com/reference/android/media/MediaCodecInfo.CodecProfileLevel)
media APIs:

*   Support for 12-bit format is OPTIONAL.

If device implementations claim to support an HDR Profile (`VP9Profile2HDR`,
`VP9Profile2HDR10Plus`, `VP9Profile3HDR`, `VP9Profile3HDR10Plus`) through the
media APIs:

*   [C-4-1] Device implementations MUST accept the required HDR metadata
    ([`MediaFormat#KEY_HDR_STATIC_INFO`](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR_STATIC_INFO)
    for all HDR profiles, as well as parameter
    [`MediaCodec#PARAMETER_KEY_HDR10_PLUS_INFO`](
    https://developer.android.com/reference/android/media/MediaCodec#PARAMETER_KEY_HDR10_PLUS_INFO)
    for `HDR10Plus` profiles) from the application using MediaCodec API, as well
    as support extracting the required HDR metadata
    ([`MediaFormat#KEY_HDR_STATIC_INFO`](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR_STATIC_INFO)
    for all HDR profiles, as well as
    [`MediaFormat#KEY_HDR10_PLUS_INFO`](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR10_PLUS_INFO)
    for `HDR10Plus` profiles) from the bitstream and/or container as defined by
    the relevant specifications. They MUST also support outputting the required
    HDR metadata
    ([`MediaFormat#KEY_HDR_STATIC_INFO`](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR_STATIC_INFO)
    for all HDR profiles) from the bitstream and/or container as defined by the
    relevant specifications.

*   [C-4-2] Device implementations MUST properly display HDR content for
    `VP9Profile2HDR` and `VP9Profile3HDR` profiles on the device screen or on a
    standard video output port (e.g., HDMI).

*   [C-SR] The device implementations are STRONGLY RECOMMENDED to support
    outputting the metadata
    [`MediaFormat#KEY_HDR10_PLUS_INFO`](
    https://developer.android.com/reference/android/media/MediaFormat.html#KEY_HDR10_PLUS_INFO)
    for `HDR10Plus` profiles via
    [`MediaCodec#getOutputFormat(int)`](
    https://developer.android.com/reference/android/media/MediaCodec#getOutputFormat%28int%29).

*   [C-SR] Device implementations are STRONGLY RECOMMENDED to properly display
    HDR content for VP9Profile2HDR10Plus and VP9Profile3HDR10Plus profiles on
    the device screen or on a standard video output port (e.g., HDMI).

### 5.3.8\.  Dolby Vision

If device implementations declare support for the Dolby Vision decoder through
[`HDR_TYPE_DOLBY_VISION`](
https://developer.android.com/reference/android/view/Display.HdrCapabilities.html#HDR_TYPE_DOLBY_VISION)
, they:

*   [C-1-1] MUST provide a Dolby Vision-capable extractor.
*   [C-1-2] MUST properly display Dolby Vision content on the device screen or
on a standard video output port (e.g., HDMI).
*   [C-1-3] MUST set the track index of backward-compatible base-layer(s) (if
present) to be the same as the combined Dolby Vision layer's track index.

### 5.3.9\. AV1

If device implementations support AV1 codec, they:

*   [C-1-1] MUST support Profile 0 including 10-bit content.
