`void GetRecommendedRenderTargetSize( uint32_t *pnWidth, uint32_t *pnHeight )`

Provides the game with the minimum size that it should use for its offscreen render target to minimize pixel stretching. This size is matched with the projection matrix and distortion function and will change from display to display depending on resolution, distortion, and field of view.
为游戏提供

* `pnWidth` - recommended width for the offscreen render target
* `pnHeight` - recommended height for the offscreen render target
