在开发过程中，应用程序应尽可能遵循 ViewModelLocator 默认命名约定，但仍有许多不遵循约定的 ViewModel，又该如何实现View和ViewModel绑定呢？
ViewModelLocator 批量自动绑定View和ViewModel正如我们上章所说，可以通过更改标准命名约定的方式实现，但在更改命名约定逻辑仍然无法满足所有命名要求的情况下，可以使用自定义ViewModel注册方法直接将 ViewModel 映射到特定视图 ViewModelLocationProvider.Register 。

```C#

public class MainModule : IModule
{
 public static void RegisterTypes(IContainerRegistry containerRegistry)
 {
 ViewModelLocationProvider.Register<ALNoiseGateView, NoiseGateViewModel>();
 ViewModelLocationProvider.Register<ALCompressorView, CompressorViewModel>();
 ViewModelLocationProvider.Register<ALLimiterView, LimiterViewModel>();
 }

}


```
同时在View中需要设置
```http
xmlns:prism="http://prismlibrary.com/"
  prism:ViewModelLocator.AutoWireViewModel="True"
```