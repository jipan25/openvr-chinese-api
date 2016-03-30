# 概述
OpenVR API为游戏或应用提供了一种不依赖于各种硬件平台的VR显示器交互接口。它可以在不影响游戏代码的同时实现软硬件接口的独立更新。

API是一组C++接口类的纯虚函数。当应用程序初始化VR系统后，它将返回一个接口，这个接口提供匹配了SDK中所有在头文件里定义的方法。一旦某个版本的API接口被发布了，它将在之后所有版本中得到支持，所以应用程序不需要更新到新的sdk就可以得到新硬件或其它功能的支持。
# 初始化和清理
Because the OpenVR API causes the game to connect to any attached VR hardware, it is not initialized automatically. To initialize the API and get access to the vr::IVRSystem interface call the openvr::VR_Init function. To close down your connection to the hardware and release your vr::IVRSystem interface, call openvr::VR_Shutdown.
由于OpenVR API使游戏连接到任意的VR硬件，它不会自动初始化。如果要初始化API得到访问vr::IVRSystem的接口，需调用openvr::VR_Init函数。如果要释放vr::IVRSystem接口，关闭你的程序到硬件的连接，执行openvr::VR_Shutdown函数。

`vr::IVRSystem *openvr::VR_Init( vr::`[`HmdError`](https://github.com/ValveSoftware/openvr/wiki/HmdError)` *peError )`

The call will return a vr::IVRSystem pointer that allows the game to call other OpenVR API methods. If something fails the call will return NULL and peError will be set to an error code that indicates what the problem was.
peError - The error code that occurred or vr::HmdError_None if there was no error. See [`vr::HmdError`](https://github.com/ValveSoftware/openvr/wiki/HmdError) for possible error codes.
这个调用将返回一个vr::IVRSystem的指针，允许游戏调用其它OpenVR API的方法。如果调用过程出错，会返回空指针NULL和一个peError，peError会被设置为一个错误码表明是什么问题。

`void openvr::VR_Shutdown()`

Shuts down the connection to the VR hardware and cleans up the OpenVR API. The vr::IVRSystem pointer returned by vr::VR_Init will be invalid after this call is made. 


# Interfaces

The API is broken down into 3 primary interfaces in the vr namespace:
* [IVRSystem](https://github.com/ValveSoftware/openvr/wiki/IVRSystem_Overview) - Main interface for display, distortion, tracking, controller, and event access.
* [IVRChaperone](https://github.com/ValveSoftware/openvr/wiki/IVRChaperone_Overview) - Provides access to chaperone soft and hard bounds.
* [IVRCompositor](https://github.com/ValveSoftware/openvr/wiki/IVRCompositor_Overview) - Allows an application to render 3D content through the VR compositor.
* [IVROverlay](https://github.com/ValveSoftware/openvr/wiki/IVROverlay_Overview) - Allows an application to render 2D content through the VR Compositor.
* [IVRRenderModels](https://github.com/ValveSoftware/openvr/wiki/IVRRenderModels_Overview) - Allows an application access to render models.

# Other Functions

`bool openvr::VR_IsHmdPresent()`

Returns true if the system believes that an HMD is present on the system. This function is much faster than initializing all of OpenVR just to check for an HMD. Use it when you have a piece of UI that you want to enable only for users with an HMD.

This function will return true in situations where vr::VR_Init() will return NULL. It is a quick way to eliminate users that have no VR hardware, but there are some startup conditions that can only be detected by starting the system.


`const char *VR_GetStringFor HmdError( vr::HmdError error );`

This function returns an English translation of vr::HmdError enum values. It can be called any time, regardless of whether the VR system is started up.


`void *VR_GetGenericInterface( const char *pchInterfaceVersion, vr::`[`HmdError`](https://github.com/ValveSoftware/openvr/wiki/HmdError)` *peError )`

Requests an interface by name from OpenVR. It will return NULL and pass back an error in peError if the interface can't be found. It will always return NULL if openvr::VR_Init() has not been called successfully.
