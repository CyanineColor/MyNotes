日志打印记录
在序列化失败的时候，通过打赢过程，调试判断序列化异常的数据
```C#
var settings = new JsonSerializerSettings 
{ 
TraceWriter = new MemoryTraceWriter() 记录序列化过程:ml-citation
{ref="5,7" data="citationList"} }; 
JsonConvert.SerializeObject(myObject, settings); Console.WriteLine(settings.TraceWriter);
```

Json字符串操作
```C#
```csharp
/ 1. 从字符串加载
        string json = @"{'name':'Tom','age':20,'skills':['C#','Redis']}";

        JObject obj = JObject.Parse(json);

        // 2. 取值
        string name = (string)obj["name"];
        int    age  = (int)obj["age"];
        Console.WriteLine($"{name} is {age}");

        // 3. 改值 / 新增
        obj["age"]   = 21;
        obj["email"] = "tom@abc.com";

        // 4. 遍历数组
        foreach (var s in obj["skills"])
            Console.WriteLine("skill:" + s);

        // 5. 输出回字符串
        string newJson = obj.ToString();
        Console.WriteLine(newJson);
```
```

1. 最简原型
    


```csharp
public void Merge(JObject source,
                  JsonMergeSettings? settings = null)
```

---

2. Merge（）默认行为 （不写 settings）
    

- **同名键** → **直接覆盖**（原值丢失）
    
- **嵌套对象** → **递归合并**
    
- **数组** → **整组替换**（不会追加元素）