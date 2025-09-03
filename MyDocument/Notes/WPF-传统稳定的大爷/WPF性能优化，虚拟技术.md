## 前言
当在一个ItemsControl（或继承自ItemsControl）控件中绑定一个集合的时候，如果集合中的条目过多，那么界面就会变得卡顿甚至停止响应，特别是在容器或窗口大小发生改变时，界面的渲染就会给人一种慢半拍的感觉，体验感非常差，这时我们就可以用虚拟化技术来解决这个问题。  

    UI虚拟化的核心思想就是只渲染可视范围内的控件，所以它通常会搭配ScrollViewer控件一起使用，通过ScrollViewer控件中的VerticalOffset、HorizontalOffset、ViewportWidth、ViewportHeight等参数可以计算出在可视范围内应该显示的控件，当控件不被显示时将它从Panel中移出，这样就可以保证同一时间只渲染了有限的控件，而不是渲染所有控件，从而达到性能提升的目的。
   1. **核心思想**‌  
    仅创建和渲染当前可见区域的UI元素，通过动态回收/生成容器对象减少内存占用和渲染压力。例如当列表包含1000项时，仅生成可视范围内的20-30个容器元素，滚动时回收不可见元素并生成新元素。
    **关键技术组件**
    ‌VirtualizingStackPanel‌：默认支持虚拟化的布局容器，基于StackPanel扩展，通过VirtualizingPanel.IsVirtualizing="True"属性启用13。
‌ScrollViewer‌：必须设置ScrollViewer.CanContentScroll="True"确保基于逻辑单元滚动（虚拟化必要条件）68。
### 虚拟化实现方式
```C#
<ListBox VirtualizingPanel.IsVirtualizing="True"
         ScrollViewer.CanContentScroll="True">
    <ListBox.ItemsPanel>
        <ItemsPanelTemplate>
            <VirtualizingStackPanel VirtualizationMode="Recycling"/>
        </ItemsPanelTemplate>
    </ListBox.ItemsPanel>
</ListBox>

```

常见陷阱
- **样式覆盖**‌：若控件模板中未包含ScrollViewer或设置`OverridesDefaultStyle="True"`会禁用虚拟化6。
- ‌**数据绑定类型**‌：仅直接绑定到`ItemsSource`（而非嵌套集合）时虚拟化生效
-

**VirtualizationMode**‌：`Standard`（默认）每次滚动生成新容器，`Recycling`复用容器提升性能

VirtualizingPanel中除了IsVirtualizing参数以外还有很多其它参数可以控制更多的虚拟化细节，以下是参数说明：

1). VirtualizingPanel.CacheLength="10"

作用：CacheLength 属性指定了在虚拟化过程中，控件需要缓存的项目数。这意味着在视口之外的区域中，面板会保留一定数量的项目以提高滚动平滑度。当用户滚动视图时，缓存的项目可以更快地重新使用，从而减少重新创建和布局的开销。

值：10 表示视口外会缓存 10 个项目。这是一个相对的值，具体数目可能会根据实际实现有所不同。

2). VirtualizingPanel.CacheLengthUnit="Item"

作用：CacheLengthUnit 属性定义 CacheLength 的单位。可以选择 Pixel 或 Item，其中 Item 表示缓存的长度以项目的数量为单位，Pixel 表示缓存的长度以像素为单位。

值：Item 表示缓存的长度是以项目的数量为单位。这适用于项目大小固定或数据量较小的情况。

3). VirtualizingPanel.IsContainerVirtualizable="True"

作用：IsContainerVirtualizable 属性指示面板是否允许对其子项的容器进行虚拟化。设置为 True 表示面板可以对其容器进行虚拟化，从而优化性能，特别是在处理大量数据时。

值：True 表示启用容器虚拟化。

4). VirtualizingPanel.IsVirtualizing="True"

作用：IsVirtualizing 属性指示面板是否启用虚拟化。这是虚拟化的核心设置，设置为 True 表示面板会仅对视口内的项目进行渲染和处理，而不是一次性加载所有项目。

值：True 表示启用虚拟化，减少不必要的控件实例化和布局计算。

5). VirtualizingPanel.IsVirtualizingWhenGrouping="True"

作用：IsVirtualizingWhenGrouping 属性控制面板在分组时是否继续进行虚拟化。当设置为 True 时，面板在分组数据时仍然会应用虚拟化策略，以保持性能优化。

值：True 表示即使在数据分组时，也保持虚拟化。

6). VirtualizingPanel.ScrollUnit="Item"

作用：ScrollUnit 属性定义滚动的单位。可以选择 Item 或 Pixel，其中Item 表示每次滚动一个项目，Pixel 表示每次滚动一定像素。

值：Item 表示每次滚动一个项目的单位，而不是固定像素数，这对于项目高度一致的情况尤其有效。

7). VirtualizingPanel.VirtualizationMode="Recycling"

作用：VirtualizationMode 属性指定虚拟化模式。Recycling 模式表示控件会重用已经不再可见的项目的容器，而不是销毁它们。这种方式可以减少控件的创建和销毁开销，从而提升性能。

值：Recycling 表示启用重用模式，使面板更高效地管理控件实例，适合动态数据变化的场景。

### 性能对比数据
- **无虚拟化**‌：加载10000项时内存占用约200MB，滚动卡顿明显。
- ‌**启用虚拟化**‌：内存占用降至30MB，滚动帧率提升至60FPS36。
通过合理配置虚拟化技术，可显著提升WPF应用处理大数据集时的响应速度与用户体验。

