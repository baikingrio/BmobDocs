# Bmob文档中心 #
基于 [MkDocs][1] 的 Bmob 文档中心, [在线预览](https://baikingrio.github.io/bmobdocs/)

## 目录结构说明 ##

	|-- assets                            // 文档中心所需的静态资源
	|-- mkdocs                           // mkdocs 编辑文档的工作目录
	|   |-- service                         // Bmob各服务文档
	|       |-- cloudcode                   // 云端逻辑文档 (内容与数据服务文档类似)
	|       |-- container                   // 容器服务文档 (内容与数据服务文档类似)
	|       |-- data                        // 数据服务文档
	|           |-- android            // 数据服务Android文档
	|               |-- docs               // 包含文档源文件的目录
    |                   |-- image               // 文档首页index.md文件中用到的图片资源
	|                   |-- module             // 文档首页以外的其他文档
	|                       |-- auto_update         // Android的自动更新文档
	|                           |-- image               // Android自动更新文档中用到的图片资源
	|                           |-- README.md           // Android自动更新文档源文件
	|                       |-- class_doc           // Android SDK 类库文档 (内容与auto_update目录结构类似)
	|                       |-- develop_doc         // Android SDK 开发文档 (内容与auto_update目录结构类似)
	|                       |-- example             // Android SDK 示例和功能文档 (内容与auto_update目录结构类似)
	|                       |-- update_log          // Android SDK 更新日志文档 (内容与auto_update目录结构类似)
	|                   |-- index.md           // 默认的文档首页 (这里使用的Android快速入门文档)
	|               |-- mkdocs.yml             // mkdocs 配置文件
	|           |-- cocos2d-x       // 数据服务Cocos2d-x文档 (内容与数据服务Android文档目录结构一样)
	|           |-- csharp          // 数据服务C#文档 (内容与数据服务Android文档目录结构一样)
	|           |-- go              // 数据服务Go文档 (内容与数据服务Android文档目录结构一样)
	|           |-- ios             // 数据服务iOS文档 (内容与数据服务Android文档目录结构一样)
	|           |-- javascript      // 数据服务JavaScript文档 (内容与数据服务Android文档目录结构一样)
	|           |-- php             // 数据服务PHP文档 (内容与数据服务Android文档目录结构一样)
	|           |-- restful         // 数据服务Restful文档 (内容与数据服务Android文档目录结构一样)
	|           |-- wechat-app      // 数据服务微信小程序文档 (内容与数据服务Android文档目录结构一样)
	|       |-- im          // IM服务文档 (内容与数据服务文档类似)
	|       |-- other       // 其他文档 (内容与数据服务文档类似)
	|       |-- pay         // 支付服务文档 (内容与数据服务文档类似)
	|       |-- push        // 推送服务文档 (内容与数据服务文档类似)
	|       |-- sms         // 短信服务文档 (内容与数据服务文档类似)
	|-- service                              // mkdocs编译后的文档静态页面
	|       |-- cloudcode                   // 云端逻辑文档
	|       |-- container                   // 容器服务文档
	|       |-- data                        // 数据服务文档
	|           |-- android                     // 数据服务Android文档经过mkdocs编译后输出的静态页面
	|           |-- cocos2d-x                   // 数据服务Cocos2d-x文档经过mkdocs编译后输出的静态页面
	|           |-- csharp                      // 数据服务C#文档经过mkdocs编译后输出的静态页面
	|           |-- go                          // 数据服务Go文档经过mkdocs编译后输出的静态页面
	|           |-- ios                         // 数据服务iOS文档经过mkdocs编译后输出的静态页面
	|           |-- javascript                  // 数据服务JavaScript文档经过mkdocs编译后输出的静态页面
	|           |-- php                         // 数据服务PHP文档经过mkdocs编译后输出的静态页面
	|           |-- restful                     // 数据服务Restful文档经过mkdocs编译后输出的静态页面
	|           |-- wechat-app                  // 数据服务微信小程序文档经过mkdocs编译后输出的静态页面
	|       |-- im                          // IM服务文档
	|       |-- other                       // 其他文档
	|       |-- pay                         // 支付服务文档
	|       |-- push                        // 推送服务文档
	|       |-- sms                         // 短信服务文档
	|-- favicon.ico                    // 网页图标
	|-- index.html                     // 文档中心首页
	|-- README.md                      // 项目说明

## MkDocs 常用命令 ##

 - 创建 mkdocs 项目

```bash
mkdocs new my-project
cd my-project
```
 有一个配置文件 mkdocs.yml, 和一个包含文档源码的 docs 文件夹. 在 docs 文件夹里包含了一个名为  index.md 的文档.
 
 - 启动内建服务器

```bash
mkdocs serve
Running at: http://127.0.0.1:8000/
```
在浏览器中打开 http://127.0.0.1:8000/ , 预览默认文档项目。

 - 站点生成
```bash
mkdocs build --clean
```

## MkDocs 配置文件 ##
```yaml
site_name: MkLorum  # 网页标题
pages:
- [index.md, Home]      # 导航栏目Home
- [about.md, About]     # 导航栏目About
```

其他详细配置可参考MkDocs 中文文档 配置部分

## 其他LINKS ##

[MkDocs 官网][1]

[MkDocs Github][2]

[MkDocs 中文文档][3]


  [1]: http://www.mkdocs.org/ "MkDocs 官网"
  [2]: https://github.com/mkdocs/mkdocs/ "MkDocs Github"
  [3]: http://markdown-docs-zh.readthedocs.io/zh_CN/latest/ "MkDocs 中文文档"