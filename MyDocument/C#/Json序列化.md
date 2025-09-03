日志打印记录
在序列化失败的时候，通过打赢过程，调试判断序列化异常的数据
```C#
var settings = new JsonSerializerSettings 
{ 
TraceWriter = new MemoryTraceWriter() 记录序列化过程:ml-citation
{ref="5,7" data="citationList"} }; 
JsonConvert.SerializeObject(myObject, settings); Console.WriteLine(settings.TraceWriter);
```