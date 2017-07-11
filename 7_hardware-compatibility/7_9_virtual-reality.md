## 7.9\. Virtual Reality

Android includes APIs and facilities to build "Virtual Reality" (VR) applications including high
quality mobile VR experiences. Device implementations MUST properly implement these APIs and
behaviors, as detailed in this section.

### 7.9.1\. Virtual Reality Mode

Android handheld device implementations that support a mode for VR applications that handles
stereoscopic rendering of notifications and disable monocular system UI components while a VR
application has user focus MUST declare `android.software.vr.mode` feature. Devices declaring this
feature MUST include an application implementing `android.service.vr.VrListenerService` that can be
enabled by VR applications via `android.app.Activity#setVrModeEnabled`.

### 7.9.2\. Virtual Reality High Performance

Android handheld device implementations MUST identify the support of high performance virtual
reality for longer user periods through the `android.hardware.vr.high_performance` feature flag and
meet the following requirements.

*   Device implementations MUST have at least 2 physical cores.
*   Device implementations MUST declare android.software.vr.mode feature.
*   Device implementations MAY provide an exclusive core to the foreground
    application and MAY support the Process.getExclusiveCores API to return
    the numbers of the cpu cores that are exclusive to the top foreground
    application. If exclusive core is supported then the core MUST not allow
    any other userspace processes to run on it (except device drivers used
    by the application), but MAY allow some kernel processes to run as
    necessary.
*   Device implementations MUST support sustained performance mode.
*   Device implementations MUST support OpenGL ES 3.2.
*   Device implementations MUST support Vulkan Hardware Level 0 and SHOULD support
    Vulkan Hardware Level 1.
*   Device implementations MUST implement
    [EGL_KHR_mutable_render_buffer](https://www.khronos.org/registry/EGL/extensions/KHR/EGL_KHR_mutable_render_buffer.txt),
    [EGL_ANDROID_front_buffer_auto_refresh](https://www.khronos.org/registry/EGL/extensions/ANDROID/EGL_ANDROID_front_buffer_auto_refresh.txt),
    [EGL_ANDROID_get_native_client_buffer](https://www.khronos.org/registry/EGL/extensions/ANDROID/EGL_ANDROID_get_native_client_buffer.txt),
    [EGL_KHR_fence_sync](https://www.khronos.org/registry/EGL/extensions/KHR/EGL_KHR_fence_sync.txt),
    [EGL_KHR_wait_sync](https://www.khronos.org/registry/EGL/extensions/KHR/EGL_KHR_wait_sync.txt),
    [EGL_IMG_context_priority](https://www.khronos.org/registry/EGL/extensions/IMG/EGL_IMG_context_priority.txt),
    [EGL_EXT_protected_content](https://www.khronos.org/registry/EGL/extensions/EXT/EGL_EXT_protected_content.txt),
    and expose the extensions in the list of available EGL extensions.
*   The GPU and display MUST be able to synchronize access to the shared front buffer such that
    alternating-eye rendering of VR content at 60fps with two render contexts will be displayed with
    no visible tearing artifacts.
*   Device implementations MUST implement
    [GL_EXT_multisampled_render_to_texture](https://www.khronos.org/registry/OpenGL/extensions/EXT/EXT_multisampled_render_to_texture.txt),
    [GL_OVR_multiview](https://www.khronos.org/registry/OpenGL/extensions/OVR/OVR_multiview.txt),
    [GL_OVR_multiview2](https://www.khronos.org/registry/OpenGL/extensions/OVR/OVR_multiview2.txt),
    [GL_OVR_multiview_multisampled_render_to_texture](https://www.khronos.org/registry/OpenGL/extensions/OVR/OVR_multiview_multisampled_render_to_texture.txt),
    [GL_EXT_protected_textures ](https://www.khronos.org/registry/OpenGL/extensions/EXT/EXT_protected_textures.txt),
    and expose the extensions in the list of available GL extensions.
*   Device implementations MUST implement support for [AHardwareBuffer](https://developer.android.com/ndk/reference/hardware__buffer_8h.html)
    flags `AHARDWAREBUFFER_USAGE_GPU_DATA_BUFFER` and `AHARDWAREBUFFER_USAGE_SENSOR_DIRECT_DATA` as
    described in the NDK.
*   Device implementations MUST implement support for `AHardwareBuffers` with more than one layer.
*   Device implementations MUST support H.264 decoding at least 3840x2160@30fps-40Mbps (equivalent
    to 4 instances of 1920x1080@30fps-10Mbps or 2 instances of 1920x1080@60fps-20Mbps).
*   Device implementations MUST support HEVC and VP9, MUST be capable to decode at least
    1920x1080@30fps-10Mbps and SHOULD be capable to decode 3840x2160@30fps-20Mbps (equivalent to
    4 instances of 1920x1080@30fps-5Mbps).
*   The device implementations are STRONGLY RECOMMENDED to support
    android.hardware.sensor.hifi_sensors feature and MUST meet the gyroscope, accelerometer, and
    magnetometer related requirements for android.hardware.hifi_sensors.
*   Device implementations MUST support HardwarePropertiesManager.getDeviceTemperatures API and
    return accurate values for skin temperature.
*   The device implementation MUST have an embedded screen, and its resolution MUST be at least be
    FullHD(1080p) and STRONGLY RECOMMENDED TO BE  be QuadHD (1440p) or higher.
*   The display MUST measure between 4.7" and 6.3" diagonal.
*   The display MUST update at least 60 Hz while in VR Mode.
*   The display latency on Gray-to-Gray, White-to-Black, and Black-to-White switching time MUST
    be ≤ 3 ms.
*   The display MUST support a low-persistence mode with ≤5 ms persistence,persistence being
    defined as the amount of time for which a pixel is emitting light.
*   Device implementations MUST support Bluetooth 4.2 and Bluetooth LE Data Length Extension
    [section 7.4.3](#7_4_3_bluetooth).
