## CancellationTokenSource
### ‌**作用**‌

1. ‌**取消信号源**‌：生成并管理 `CancellationToken`，通过它向任务发送取消请求。
2. ‌**协作式取消**‌：允许任务“优雅退出”，而非强制终止，避免资源泄漏或不一致状态。
3. ‌**支持超时和组合取消**‌：可设置自动取消的超时时间，或合并多个取消信号。
### **任务中的取消检查**‌

任务需主动监听取消请求，通过以下方式
```c#
void DoWork(CancellationToken token) 
{ 
while (true) 
{ // 方式1：检查取消标记并退出
if (token.IsCancellationRequested) break; 
// 方式2：直接抛出 OperationCanceledException 
token.ThrowIfCancellationRequested(); 
// ... 执行工作 ... } 
}
```
#### **用户主动取消操作**‌

- ‌**场景**‌：例如UI界面上的“取消”按钮，用户点击后停止后台任务。
- ‌**代码示例**‌：
```c#
-private CancellationTokenSource _cts; 
private async void StartButton_Click(object sender, EventArgs e) 

{ _cts = new CancellationTokenSource(); 
try
{ await Task.Run(() => LongRunningOperation(_cts.Token), _cts.Token); }
catch (OperationCanceledException) 
{
MessageBox.Show("任务已取消。"); 
} 
} 
private void CancelButton_Click(object sender, EventArgs e)
{ _cts?.Cancel(); }
```
####  ‌**超时自动取消**‌

- ‌**场景**‌：限制任务执行时间，避免无限等待。
- ‌**代码示例**‌：
```c#
- var cts = new CancellationTokenSource(5000); 
- // 5秒后自动取消 
- try 
- { await SomeAsyncMethod(cts.Token); } 
- catch (TaskCanceledException)
- { 
- Console.WriteLine("操作超时！"); 
- }
```