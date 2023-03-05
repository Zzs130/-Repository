# .net

[TOC]

## Visual Studio技巧

### 注释及Visual Studio快捷键

> //单行注释
> ///文档注释，解释类、方法
>/*
>多行注释
>*/

### 快捷键

Ctrl+k+d 快速对齐
Ctrl+z 撤销
Ctrl+s 保存
Ctrl+j 快速弹出智能提示、
Ctrl+m+o 折叠所有注释
Ctrl+m+p 展开所有注释
Shift+Alt+. 快速修复

## C#数据类型

### 值类型Value Type

类型|描述|范围|默认值
:-|:---|--|--
bool|布尔值|True或false|False
byte|8位无符号整数|0到255|0
char|16位Unicode（统一码）字符|U +0000到U +ffff|'\0'
<https://www.runoob.com/csharp/csharp-data-types.html>

#### byte字节 bit位 Word字

1 byte=8bit
bit=位
byte=字节
Word=字
32位计算机：1字=32位=4字节
64位计算机：1字=64位=8字节

### int

### string

### Dynamic 动态类型

### using

<https://blog.csdn.net/wanderocn/article/details/6659811>

## SQL server使用

### 数据库连接

>String constr = "server=192.168.1.108;database=postal;Integrated Security=False;user id=sa;password=123123;Connection Timeout=30";
SqlConnection myconnn =new SqlConnection(constr);
static string sql = "select * from dbo.PostalCode";
//打开
myconn.Open();
//执行
SqlCommand cmd = new SqlCommand(sql, myconnn);
//关闭
myconn.Close();

## 常用api

### System.IO

>Stream:以流方式操作资源的抽象类
>>FileStream:以字节为单位操作文件的类
MemoryStream:以字节为单位操作内存的类
NetworkStream:以字符为单位操作网络的类

## 后台控制应用

![后台控制应用](\Snipaste_2022-09-10_13-31-44.JPG)

项目BasicsStudy后台控制应用项目位置
D:\Documents\C#dome\Study

## 项目发布需要安装一大堆

根据项目安装对应的sdk或honsting,.net 3.0 sdk .net6.0 sdk asp.net core 5.0等
redis

win8.1 iis 500.19 0x8007000d错误，
解决办法：安装.net core runtime，看自己程序是什么版本的.net core，最好是跟自己源代码使用的.net core版本一致，挂在IIS上的是需要下载Hosting Bundle版的。

## 代码精简优化

<https://www.cnblogs.com/linJie1930906722/p/5349580.html>

## 读写

excel
<https://blog.csdn.net/qq_34202873/article/details/87629139>

理解
<https://www.jianshu.com/p/fa7bdc4f3de7>

可用类
<https://www.cnblogs.com/mcad/p/4203550.html>
<https://www.cnblogs.com/shuang121/archive/2011/11/10/2244438.html>
案例
<https://www.cnblogs.com/liqingwen/p/6082673.html>

## entityFramework

### 常见错误

新增数据时，出现的错误
错误原因是sqlserver中的表与webapi的表数据类型不一致，如sql中id是int,webapi中id是long

```ts
Microsoft.EntityFrameworkCore.DbUpdateException: An error occurred while saving the entity changes. See the inner exception for details.
 ---> System.InvalidCastException: Unable to cast object of type 'System.Int32' to type 'System.Int64'.
   at Microsoft.Data.SqlClient.SqlBuffer.get_Int64()
   at lambda_method31(Closure , DbDataReader , Int32 )
   at Microsoft.EntityFrameworkCore.RelationalPropertyExtensions.GetReaderFieldValue(IProperty property, RelationalDataReader relationalReader, Int32 ordinal, Boolean detailedErrorsEnabled)
   at Microsoft.EntityFrameworkCore.Update.ModificationCommand.PropagateResults(RelationalDataReader relationalReader)
   at Microsoft.EntityFrameworkCore.Update.AffectedCountModificationCommandBatch.ConsumeResultSet(Int32 startCommandIndex, RelationalDataReader reader)
   at Microsoft.EntityFrameworkCore.Update.AffectedCountModificationCommandBatch.Consume(RelationalDataReader reader)
   --- End of inner exception stack trace ---
   at Microsoft.EntityFrameworkCore.Update.AffectedCountModificationCommandBatch.Consume(RelationalDataReader reader)
   at Microsoft.EntityFrameworkCore.Update.ReaderModificationCommandBatch.Execute(IRelationalConnection connection)
   at Microsoft.EntityFrameworkCore.SqlServer.Update.Internal.SqlServerModificationCommandBatch.Execute(IRelationalConnection connection)
   at Microsoft.EntityFrameworkCore.Update.Internal.BatchExecutor.Execute(IEnumerable`1 commandBatches, IRelationalConnection connection)
   at Microsoft.EntityFrameworkCore.ChangeTracking.Internal.StateManager.SaveChanges(IList`1 entriesToSave)
   at Microsoft.EntityFrameworkCore.ChangeTracking.Internal.StateManager.SaveChanges(StateManager stateManager, Boolean acceptAllChangesOnSuccess)
   at Microsoft.EntityFrameworkCore.SqlServer.Storage.Internal.SqlServerExecutionStrategy.Execute[TState,TResult](TState state, Func`3 operation, Func`3 verifySucceeded)
   at Microsoft.EntityFrameworkCore.ChangeTracking.Internal.StateManager.SaveChanges(Boolean acceptAllChangesOnSuccess)
   at Microsoft.EntityFrameworkCore.DbContext.SaveChanges(Boolean acceptAllChangesOnSuccess)
   at TodoApi.Server.TestServer.Conut() in D:\Documents\C#dome\Study\BasicsStudy\TodoApi\Server\TestServer.cs:line 25
   at TodoApi.Controllers.TestController.Get1() in D:\Documents\C#dome\Study\BasicsStudy\TodoApi\Controllers\TestController.cs:line 25
   at lambda_method2(Closure , Object , Object[] )
   at Microsoft.AspNetCore.Mvc.Infrastructure.ActionMethodExecutor.SyncObjectResultExecutor.Execute(IActionResultTypeMapper mapper, ObjectMethodExecutor executor, Object controller, Object[] arguments)
   at Microsoft.AspNetCore.Mvc.Infrastructure.ControllerActionInvoker.InvokeActionMethodAsync()
   at Microsoft.AspNetCore.Mvc.Infrastructure.ControllerActionInvoker.Next(State& next, Scope& scope, Object& state, Boolean& isCompleted)
   at Microsoft.AspNetCore.Mvc.Infrastructure.ControllerActionInvoker.InvokeNextActionFilterAsync()
--- End of stack trace from previous location ---
   at Microsoft.AspNetCore.Mvc.Infrastructure.ControllerActionInvoker.Rethrow(ActionExecutedContextSealed context)
   at Microsoft.AspNetCore.Mvc.Infrastructure.ControllerActionInvoker.Next(State& next, Scope& scope, Object& state, Boolean& isCompleted)
   at Microsoft.AspNetCore.Mvc.Infrastructure.ControllerActionInvoker.InvokeInnerFilterAsync()
--- End of stack trace from previous location ---
   at Microsoft.AspNetCore.Mvc.Infrastructure.ResourceInvoker.<InvokeFilterPipelineAsync>g__Awaited|20_0(ResourceInvoker invoker, Task lastTask, State next, Scope scope, Object state, Boolean isCompleted)
   at Microsoft.AspNetCore.Mvc.Infrastructure.ResourceInvoker.<InvokeAsync>g__Awaited|17_0(ResourceInvoker invoker, Task task, IDisposable scope)
   at Microsoft.AspNetCore.Mvc.Infrastructure.ResourceInvoker.<InvokeAsync>g__Awaited|17_0(ResourceInvoker invoker, Task task, IDisposable scope)
   at Microsoft.AspNetCore.Routing.EndpointMiddleware.<Invoke>g__AwaitRequestTask|6_0(Endpoint endpoint, Task requestTask, ILogger logger)
   at Microsoft.AspNetCore.Authorization.AuthorizationMiddleware.Invoke(HttpContext context)
   at Swashbuckle.AspNetCore.SwaggerUI.SwaggerUIMiddleware.Invoke(HttpContext httpContext)
   at Swashbuckle.AspNetCore.Swagger.SwaggerMiddleware.Invoke(HttpContext httpContext, ISwaggerProvider swaggerProvider)
   at Microsoft.AspNetCore.Diagnostics.DeveloperExceptionPageMiddleware.Invoke(HttpContext context)

HEADERS
=======
Accept: text/plain
Host: localhost:7129
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36 Edg/109.0.1518.70
:method: POST
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Origin: https://localhost:7129
Referer: https://localhost:7129/swagger/index.html
Content-Length: 0
sec-ch-ua: "Not_A Brand";v="99", "Microsoft Edge";v="109", "Chromium";v="109"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
sec-fetch-site: same-origin
sec-fetch-mode: cors
sec-fetch-dest: empty
```

## 多线程

## Task

## json序列化

反射，泛型、linq、
