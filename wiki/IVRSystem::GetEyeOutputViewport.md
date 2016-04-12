`void GetEyeOutputViewport( Hmd_Eye eEye, GraphicsAPIConvention eAPIType, uint32_t *pnX, uint32_t *pnY, uint32_t *pnWidth, uint32_t *pnHeight )`

Returns the viewport in pixels in display space that the game should render into for the specified eye.
返回特定眼睛的观察口对应显示空间的像素数据

* `eEye` - Eye_Left or Eye_Right. 决定返回哪只眼睛的观察口。Determines which eye the function should return the viewport for.
* `eAPIType` - 匹配对应转换API返回相应修改值。Modifies the return values to match the conventions of the specified API. One of:
  * `API_DirectX`
  * `API_OpenGL
* `pnX` - X position of the eye's viewport within the window
* `pnY` - Y position of the eye's viewport within the window
* `pnWidth` - width of the eye's viewport within the window
* `pnHeight` - height of the eye's viewport within the window
