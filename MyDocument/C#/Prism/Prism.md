## 一、应用启动流程：框架的初始化脉络

Prism应用的启动遵循严格的**三层继承体系**[](https://edu.51cto.com/article/note/26342.html)：

复制

```
WPF Application 
    ↓
PrismApplicationBase (抽象基类) 
    ↓
PrismApplication (你的App.xaml.cs)
```

### 启动的关键步骤：

1. **CreateShell()** (必须重写)
    
    - 创建主窗口（`MainWindow`），框架会自动将其显示
        
    - 这是应用的入口点，返回的窗口将承载所有区域
        
2. **RegisterTypes()** (必须重写)
    
    - 注册**全局共享服务**（如日志、配置服务）
        
    - 与模块的`RegisterTypes()`区别在于：这里注册的是跨模块的基础服务
        
3. **ConfigureModuleCatalog()** (可选重写)
    
    - 加载模块清单（ModuleCatalog），决定哪些模块被加载
        
    - 支持静态加载（代码注册）或动态加载（从目录扫描DLL）
        
4. **InitializeModules()**
    
    - 调用每个模块的`Initialize()`方法，触发模块的依赖注册
        

**启动顺序**

：

`App构造函数 → CreateShell() → RegisterTypes() → 加载模块 → 初始化模块 → 显示Shell`

---

## 二、依赖注入：框架的"血液循环系统"

### 核心机制

DI是Prism实现**松耦合架构**的基石

。框架通过抽象接口`IContainerExtension`屏蔽底层容器差异（Unity/Autofac/DryIoc），提供统一的注册/解析API。

### 注册阶段

csharp

复制

```csharp
// 在App.xaml.cs或模块中
containerRegistry.RegisterSingleton<ILoggingService, LoggingService>(); // 单例
containerRegistry.Register<IHardwareService, HardwareService>();        // 瞬态
containerRegistry.RegisterForNavigation<ViewA, ViewAViewModel>();      // 导航注册
```

**生命周期管理**

：

- **Transient**：每次解析创建新实例（默认）
    
- **Singleton**：全局唯一实例（推荐用于服务类）
    
- **Scoped**：在特定作用域（如导航请求）内共享
    

### 解析阶段

Prism在三个关键时机自动解析依赖：

1. **ViewModel构造函数注入**：创建ViewModel时自动注入已注册服务
    
2. **区域导航**：通过`IRegionManager.RequestNavigate()`时解析目标View/ViewModel
    
3. **事件聚合器**：通过`IEventAggregator`订阅事件时注入发布者/订阅者
    

**模块独立注册**

： 每个模块的`RegisterTypes()`方法相当于**服务注册表**，模块间互不干扰，但通过IoC容器实现跨模块依赖解析。

---

## 三、模块化系统：应用的"细胞组织"

### 模块生命周期

csharp

复制

```csharp
public class ModuleAModule : IModule
{
    public void RegisterTypes(IContainerRegistry containerRegistry)
    {
        // 1. 注册模块内服务
        containerRegistry.RegisterSingleton<IUserService, UserService>();
        
        // 2. 注册可导航的视图（关键！）
        containerRegistry.RegisterForNavigation<UserListView>();
    }

    public void OnInitialized(IContainerProvider containerProvider)
    {
        // 3. 初始化完成后，可执行首次导航
        var regionManager = containerProvider.Resolve<IRegionManager>();
        regionManager.RequestNavigate("MainRegion", "UserListView");
    }
}
```

### 核心设计原则

1. **功能内聚**：每个模块封装独立业务功能（如用户管理、订单处理）
    
2. **延迟加载**：通过`DirectoryModuleCatalog`动态扫描DLL加载
    
    ，实现插件式架构
    
3. **依赖隔离**：模块只能访问自己注册的和全局注册的服务
    

**模块通信的三种方式**：

- **事件聚合器**：跨模块事件总线（推荐松耦合通信）
    
- **共享服务**：注册全局单例服务作为数据总线
    
- **区域导航**：通过参数传递简单数据
    

---

## 四、区域导航与UI组合："动态搭积木"

### 区域(Region)的本质

区域是**UI占位符**，通过附加属性标记在XAML中

：

xml

复制

```xml
<ContentControl prism:RegionManager.RegionName="MainRegion" />
<ItemsControl prism:RegionManager.RegionName="SidebarRegion" />
```

### 导航流程解析

当调用`regionManager.RequestNavigate("MainRegion", "UserDetailView")`时，Prism内部执行：

1. **解析视图**：从容器中获取`UserDetailView`类型（之前通过`RegisterForNavigation`注册）
    
2. **解析ViewModel**：根据命名约定（`UserDetailView`→`UserDetailViewModel`）或显式注册，创建ViewModel实例
    
3. **依赖注入**：将ViewModel构造函数中声明的依赖（如`IEventAggregator`）注入
    
4. **DataContext绑定**：将ViewModel设置为View的`DataContext`
    
5. **区域注入**：将View添加到`MainRegion`的视觉树中
    
6. **导航生命周期**：若ViewModel实现`INavigationAware`，依次调用：
    
    - `IsNavigationTarget`：是否复用现有实例
        
    - `OnNavigatedFrom`：从原视图离开
        
    - `OnNavigatedTo`：到达新视图（可接收导航参数）
        

### ViewModelLocator自动绑定机制

在XAML中设置`prism:ViewModelLocator.AutoWireViewModel="True"`后：

1. **附加属性触发**：Prism通过附加属性监听View的`Loaded`事件
    
2. **命名约定解析**：将View名（如`ViewA`）转换为ViewModel名（`ViewAViewModel`）
    
3. **容器解析**：调用`container.Resolve<ViewAViewModel>()`创建实例
    
4. **自动绑定**：设置`view.DataContext = viewModel`
    

---

## 五、事件聚合器：模块间的"神经系统"

csharp

复制

```csharp
// 定义事件
public class DeviceAddedEvent : PubSubEvent<DeviceInfo> { }

// 发布事件（在模块A）
eventAggregator.GetEvent<DeviceAddedEvent>().Publish(newDevice);

// 订阅事件（在模块B）
eventAggregator.GetEvent<DeviceAddedEvent>().Subscribe(device => {
    // 处理逻辑
});
```

**实现原理**

：`IEventAggregator`作为单例服务注册，维护一个事件类型→事件实例的字典，实现发布-订阅模式的解耦通信。

---

## 六、完整工作流程总结

以一个"设备管理应用"为例，流程如下：

1. **启动**：`App.xaml.cs`创建Shell，注册全局日志服务
    
2. **加载模块**：扫描`Modules`目录，发现`DeviceModule.dll`
    
3. **初始化模块**：调用`DeviceModule.RegisterTypes()`，注册`IDeviceService`和`DeviceListView`
    
4. **首次导航**：模块的`OnInitialized()`中执行`regionManager.RequestNavigate("ContentRegion", "DeviceListView")`
    
5. **视图呈现**：Prism解析`DeviceListView`及其`DeviceListViewModel`，注入`IEventAggregator`和`IDeviceService`
    
6. **用户操作**：点击"添加设备"，ViewModel发布`DeviceAddedEvent`
    
7. **跨模块响应**：状态模块接收事件，更新设备统计
    

---

## 七、调试与理解技巧

1. **观察容器**：在`RegisterTypes`中设置断点，查看`containerRegistry`的注册内容
    
2. **导航监听**：为`IRegionManager.NavigationService`附加`NavigationFailed`事件
    
3. **模块加载日志**：在`ConfigureModuleCatalog()`中打印加载的模块列表
    
4. **视图模型验证**：在ViewModel构造函数中验证依赖是否成功注入
    

通过理解这四个维度的协同工作，即可掌握Prism框架的运行本质：**依赖注入提供松耦合基础，模块化实现功能划分，区域导航完成动态UI组合，事件聚合器保障模块通信**。