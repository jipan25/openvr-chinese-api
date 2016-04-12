`void GetRecommendedRenderTargetSize( uint32_t *pnWidth, uint32_t *pnHeight )`

Provides the game with the minimum size that it should use for its offscreen render target to minimize pixel stretching. This size is matched with the projection matrix and distortion function and will change from display to display depending on resolution, distortion, and field of view.
为游戏提供应当使用的最小屏幕尺寸, 以使目标对像的像素拉伸降到最低。这个尺寸会与投影矩阵和失真函数相匹配，并会根据转像、变形、亮野进行显示。

* `pnWidth` - recommended width for the offscreen render target
* `pnHeight` - recommended height for the offscreen render target
