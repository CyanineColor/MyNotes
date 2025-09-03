Dorisoy.Pan 是一个基于 .NET 8 和 WebAPI 构建的文档管理系统，它集成了 Autofac、MediatR、JWT、EF Core、MySQL 8.0 和 SQL Server 等技术，以实现一个简单、高性能、稳定且安全的解决方案。

这个系统支持多种客户端，包括网站、Android、iOS 和桌面应用，覆盖了文档管理的全流程，如计划、总结、开发、模板、测试、验收、设计、需求、收藏、分享、回收站和总空间等30多种核心功能。
## 项目使用
**1、后端启动步骤**

- 使用 Visual Studio 2019 或更新版本打开解决方案文件 Dorisoy.Pan.sln。
- 在解决方案资源管理器中右键点击并选择"还原 NuGet 包"。
- 更新 Dorisoy.Pan.API 项目中的 appsettings.json 文件内的数据库连接字符串。
- 通过 Visual Studio 菜单中的"工具">"NuGet 包管理器">"包管理器控制台"，打开包管理器控制台。
- 在包管理器控制台中，设置默认项目为 Dorisoy.Pan.Domain。 在控制台中运行 Update-Database 命令以创建数据库并填充初始数据。 将 Dorisoy.Pan.API 设置为启动项目。 按 F5 键启动项目。

**2、前端启动步骤**

如果尚未安装 Node.js，请访问 https://nodejs.org，下载并全局安装 Node.js（确保版本号至少为 4.0，同时 NPM 版本至少为 3），并全局安装 TypeScript。

- 全局安装 Angular CLI：npm install -g @angular/cli 使用 Visual Code 打开项目目录 \UI。 在集成终端中运行 npm install 以初始化并安装依赖项。
- 运行 npm run start 启动 Angular 开发服务器。
- 当 Angular 开发服务器在 localhost:4200 上监听时，在浏览器中打开 http://localhost:4200/。
- 为了在本地构建并运行生产版本，请执行 ng build --prod。这将生成一个包含压缩后的 HTML、CSS 和 JS 文件的应用程序生产版本，并放置在 dist 文件夹中，该文件夹可用于部署到生产服务器。
-参考博客：#https://www.cnblogs.com/sexintercourse/p/18431127