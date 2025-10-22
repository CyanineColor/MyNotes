BAT 脚本（Batch Script）是 Windows 系统下的批处理脚本，扩展名为 `.bat` 或 `.cmd`，由一系列命令组成，用于自动化执行命令行任务。它本质上是一个文本文件，里面写的是 Windows 命令提示符（CMD）能识别的命令。

---

### ✅ BAT 脚本能做什么？

- 自动备份文件
    
- 批量重命名
    
- 启动/关闭程序
    
- 设置环境变量
    
- 调用其他程序或脚本
    
- 简单的条件判断和循环
    

---

### 🧪 示例 1：最基础的 BAT 脚本

bat

复制

```bat
@echo off
echo 你好，世界！
pause
```

**解释：**

- `@echo off`：关闭命令回显，让输出更干净。
    
- `echo`：输出文字。
    
- `pause`：暂停，等待用户按任意键继续。
    

---

### 📁 示例 2：自动备份文件夹

bat

复制

```bat
@echo off
set source=C:\Users\YourName\Documents
set backup=D:\Backup\DocsBackup_%date:~0,10%

echo 正在备份 %source% 到 %backup%...
xcopy "%source%" "%backup%" /E /I /Y
echo 备份完成！
pause
```

---

### 🔁 示例 3：带条件判断

bat

复制

```bat
@echo off
set /p user=请输入你的名字：
if "%user%"=="admin" (
    echo 欢迎管理员！
) else (
    echo 你好，%user%！
)
pause
```

---

### 🧰 常用命令速查表

表格

复制

|命令|作用|
|:--|:--|
|`echo`|输出文本|
|`set`|设置变量|
|`if`|条件判断|
|`for`|循环|
|`xcopy`|复制文件/文件夹|
|`del`|删除文件|
|`mkdir`|创建文件夹|
|`start`|启动程序或打开文件|
|`exit`|退出脚本|

---

### 📝 如何写 BAT 脚本？

1. 打开记事本（Notepad）
    
2. 输入命令
    
3. 保存为 `.bat` 文件，例如 `myscript.bat`
    
4. 双击运行，或在 CMD 中运行：`myscript.bat`
案例：清空回收站


@echo off
echo 正在强制清空回收站...
powershell -NoProfile -Command "Clear-RecycleBin -Force -ErrorAction SilentlyContinue"
echo 回收站已清空。
