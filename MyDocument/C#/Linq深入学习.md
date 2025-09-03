什么是 LINQ？
LINQ（Language Integrated Query）是 .NET 提供的一种查询工具，让我们用一种统一的方式操作各种数据，比如列表、数据库、XML 等。可以把它想象成一个“万能查询器”，不管数据在哪里，都能轻松搞定
LINQ 方法汇总

### 2.1 筛选数据

用于从数据中挑选出你需要的部分。

|方法|功能描述|示例|
|---|---|---|
|**Where**|挑出符合条件的元素|`var result = numbers.Where(n => n > 5); // 筛选出大于 5 的数字`|
|**OfType**|挑出某种类型的元素|`var result = list.OfType<string>(); // 筛选出字符串类型的元素`|

---

### 2.2 转换数据

用于将数据“变形”。

|方法|功能描述|示例|
|---|---|---|
|**Select**|将每个元素转换成新形式|`var result = numbers.Select(n => n * 2); // 每个数字乘以 2`|
|**SelectMany**|将多个小集合合并成一个大集合|`var result = sequences.SelectMany(seq => seq); // 合并多个序列`|

---

### 2.3 排序数据

用于对数据排序。

|方法|功能描述|示例|
|---|---|---|
|**OrderBy**|按升序排序|`var result = students.OrderBy(s => s.Age); // 按年龄升序排序`|
|**OrderByDescending**|按降序排序|`var result = students.OrderByDescending(s => s.Age); // 按年龄降序排序`|
|**ThenBy**|在主排序后添加次级排序|`var result = students.OrderBy(s => s.Age).ThenBy(s => s.Name); // 次级排序`|

---

### 2.4 统计数据

用于对数据进行统计或计算。

|方法|功能描述|示例|
|---|---|---|
|**Count**|统计元素数量|`var count = numbers.Count(); // 数一数有几个元素`|
|**Sum**|计算总和|`var sum = numbers.Sum(); // 所有数字加起来`|
|**Average**|计算平均值|`var avg = numbers.Average(); // 求平均值`|
|**Min/Max**|找出最小值或最大值|`var min = numbers.Min(); // 最小值`|

---

### 2.5 分组数据

用于将数据分成小组。

|方法|功能描述|示例|
|---|---|---|
|**GroupBy**|按某个条件分组|`var result = students.GroupBy(s => s.Grade); // 按年级分组`|

---

### 2.6 获取特定元素

用于访问特定位置的元素。

|方法|功能描述|示例|
|---|---|---|
|**First/FirstOrDefault**|获取第一个元素|`var first = numbers.First(); // 第一个元素`|
|**Last/LastOrDefault**|获取最后一个元素|`var last = numbers.Last(); // 最后一个元素`|
|**ElementAt**|获取指定位置的元素|`var element = numbers.ElementAt(2); // 索引为 2 的元素`|

---

### 2.7 集合操作

用于对集合进行交集、并集、差集等操作。

|方法|功能描述|示例|
|---|---|---|
|**Union**|合并两个集合并去重|`var result = list1.Union(list2); // 合并两个列表`|
|**Intersect**|获取两个集合的交集|`var result = list1.Intersect(list2); // 找出共同元素`|
|**Except**|获取两个集合的差集|`var result = list1.Except(list2); // list1 中有但 list2 中没有的元素`|

---

### 2.8 判断条件

用于判断集合是否满足某些条件。

|方法|功能描述|示例|
|---|---|---|
|**Any**|判断是否有元素满足条件|`var exists = numbers.Any(n => n > 10); // 是否有大于 10 的数字`|
|**All**|判断是否所有元素都满足条件|`var allMatch = numbers.All(n => n > 0); // 是否所有数字都大于 0`|
|**Contains**|判断是否包含某个元素|`var contains = numbers.Contains(5); // 是否包含数字 5`|

---

### 3. 高级功能与扩展

#### 3.1 生成数据

用于生成数据。

|方法|功能描述|示例|
|---|---|---|
|**Range**|生成一个整数序列|`var numbers = Enumerable.Range(1, 10); // 生成 1 到 10 的数字`|
|**Repeat**|重复生成指定值|`var repeated = Enumerable.Repeat("Hello", 5); // 生成 5 个 "Hello"`|

  `order = Enumerable.Repeat(order, 100)                               .SelectMany(arr => arr)                               .ToList();`

---

#### 3.2 转换类型

用于将数据转换成其他类型。

|方法|功能描述|示例|
|---|---|---|
|**ToArray**|转换为数组|`var array = numbers.ToArray(); // 转成数组`|
|**ToList**|转换为列表|`var list = numbers.ToList(); // 转成列表`|
|**ToDictionary**|转换为字典|`var dictionary = students.ToDictionary(s => s.Id, s => s.Name); // 转成字典`|

---

#### 3.3 冷门但实用的方法

一些不常用但非常实用的方法。

|方法|功能描述|示例|
|---|---|---|
|**DefaultIfEmpty**|如果集合为空，返回默认值|`var result = numbers.DefaultIfEmpty(0); // 如果集合为空，返回 [0]`|
|**Zip**|将两个集合合并成一个|`var result = list1.Zip(list2, (a, b) => a + b); // 对应元素相加`|

`   int[] numbers = { 1, 2, 3, 4 };   string[] words = { "one", "two", "three" };      var numbersAndWords = numbers.Zip(words, (first, second) => first + " " + second);      foreach (var item in numbersAndWords)      Console.WriteLine(item);      // This code produces the following output:      // 1 one   // 2 two   // 3 three`

## 4. 总结

LINQ 是一个强大的工具，常用方法可以满足大部分日常需求，比如筛选、排序、分组、统计等，而冷门方法则提供了更多高级功能。掌握这些方法后，你会发现处理数据变得更加简单高效！

文档引文：[微信公众平台](https://mp.weixin.qq.com/s/a215byrZqXCcaT0pTTbbvg)