# 概述
OpenVR API为游戏或应用提供了一种不依赖于各种硬件平台的VR显示器交互接口。它可以在不影响游戏代码的同时实现软硬件接口的独立更新。

API是一组C++接口类的纯虚函数。当应用程序初始化VR系统后，它将返回一个接口，这个接口提供匹配了SDK中所有在头文件里定义的方法。一旦某个版本的API接口被发布了，它将在之后所有版本中得到支持，所以应用程序不需要更新到新的sdk就可以得到新硬件或其它功能的支持。
# 初始化和清理

由于OpenVR API使游戏连接到任意的VR硬件，它不会自动初始化。如果要初始化API得到访问vr::IVRSystem的接口，需调用openvr::VR_Init函数。如果要释放vr::IVRSystem接口，关闭你的程序到硬件的连接，执行openvr::VR_Shutdown函数。

`vr::IVRSystem *openvr::VR_Init( vr::`[`HmdError`](https://github.com/ValveSoftware/openvr/wiki/HmdError)` *peError )`


这个调用将返回一个vr::IVRSystem的指针，允许游戏调用其它OpenVR API的方法。如果调用过程出错，会返回空指针NULL和一个peError，peError会被设置为一个错误码表明是什么问题。
peError - 当前错误码，或者无错误时的vr::HmdError_None.参见 [`vr::HmdError`](wiki/HmdError.md) 查看所有错误码.


`void openvr::VR_Shutdown()`


关闭程序和VR硬件的连接并清理OpenVR API. 之前vr::VR_Init调用返回的vr::IVRSystem 指针将不合法.

# 接口Interfaces

The API is broken down into 3 primary interfaces in the vr namespace:
API在vr命名空间下被分拆为3个主要的接口:
* [IVRSystem](wiki/IVRSystem_Overview.md) - 主要包括关于显示、跟踪、变形、控制器和相关事件访问在。
* [IVRChaperone](wiki/IVRChaperone_Overview.md) - 提供了对软硬件绑定结构数据的访问。
* [IVRCompositor](wiki/IVRCompositor_Overview.md) - 允许应用程序通过VR Compositer输出3D内容.
* [IVROverlay](wiki/IVROverlay_Overview) - 允许应用程序通过VR Compositor输出2D内容.
* [IVRRenderModels](wiki/IVRRenderModels_Overview) - 允许应用程序访问输出的模型.

# 其它方法Other Functions

`bool openvr::VR_IsHmdPresent()`

当系统认为头显已正常连接时返回true.这个方法比其它初始化OpenVR后检查头显要快得多，当你有一块UI只想在用户头显上显示时可以用它。

这个方法在vr::VR_Init调用返回NULL后调用会返回true.这是一个快捷的方式通知用户当前没有VR硬件，但也有一些启动状态只能在VR系统启动后被检测。


`const char *VR_GetStringFor HmdError( vr::HmdError error );`

这个方法返回vr::HmdError的枚举值的英文翻译.它可以在任何时间被调用，而不用管VR系统是否已启动。


`void *VR_GetGenericInterface( const char *pchInterfaceVersion, vr::`[`HmdError`](https://github.com/ValveSoftware/openvr/wiki/HmdError)` *peError )`

通过接口名称获得接口句柄。如果接口名称未被找到这个方法将返回NULL并给peError赋值相应的error.如果openvr::VR_Init没有被成功调胳，则此方法始终返回NULL.
