
## 平台常见问题

** Bmob有哪些优势 **  
1.在很大程度上加快了用户产品的开发速度；对后端的支持让用户有更多的时间关注用户体验方面的设计。  
2.为用户节省了服务端人员的配备和服务器租借，节省了很多成本。  
3.在游戏方面，Bmob云端数据库保存玩家游戏数据，操作非常简单，用Api可以直接操作云端数据库。

---
** Bmob有后台介绍视频吗 **  
官方视频教程地址：[视频教程](http://doc.bmob.cn/video/index.html)  
感谢Bmob用户为我们的后台录制了视频。  
视频地址：[使用 Bmob 搭建我们的第一个后端云 APP](http://www.jikexueyuan.com/course/2208.html)  
其它的基础视频：[点击查看入门教程](http://pan.baidu.com/s/1nhPkq)

---
** Bmob支持多少用户同时在线存储查询 **  
一个APP支持10w+读并发，5w+写并发

---
** 服务器端运行在什么环境下 **  
北京BGP c机房

---
** 你们的平台稳定吗 **  
Bmob采用南北双线，多路分流的方式，将服务器部署在国内外主流的大型服务器提供商中。部署时采用7层负载均衡技术，确保每个节点机房都能够承受大量的并发请求。而每个应用之间采用`Docker`容器虚拟化，确保应用之间的安全隔离性。自2013年7月创立至今，团队积累了大量的运维和服务经验，确保平台的稳定服务。 

---
** 数据放在云端安全吗 **  
1.首先，数据在传输过程中采用了`requestId` + `timestamp` + `Application Key`的一次性对称加密算法和服务端主动防御的技术，确保数据在传输过程中能够不被`Fiddler`、`Wireshark`等抓包工具恶意抓取进行分析破坏。  
2.应用之间除采用Docker虚拟化之外，系统还定期/实时做了3级容灾备份，确保数据的可用性。  
3.在软件架构层面，Bmob提供了应用层次、表层次、ACL、角色、IP白名单、签名等多种安全控制方式。如果你想更深入了解Bmob的安全架构，可以详细查看我们的[数据安全文档](http://doc.bmob.cn/other/data_safety/)。

---
** Bmob支持国外数据访问吗 **  
根据用户反馈，东南亚跟北美那边的访问速度还是可以的。欧洲那边的话，就我们的数据来看那边的访问量不是很高，但是可以访问。

---
** 你们支持什么平台 **  
1.Android、iOS和WP三种主流的移动操作系统平台  
2.Cocos2d-x和Unity两种主流的游戏引擎  
3.Js支持HTML5移动开发  
4.C#、php、Java支持PC端开发  
5.Restful开放API接口（可使用任何语言开发）

---
** 不同SDK的数据是否打通 **
当然！本质上，所有的SDK都是基于Restful开发，数据是完全打通的。

---
** 我想迁移数据到Bmob,但是user表如何迁移呢 **  
调用restapi的注册接口来插入数据就行

---
** Bmob怎么用做HTML5的数据管理后台 **  
你可以用js sdk来开发对应的html5页面，开发好之后联系我们客服，我们帮你把h5页面放到你的bmob子域名中去，给用户访问。

---
** 如何在bmob后端构建代码来获取融云的token **  
参考代码如下：

```
function onRequest(request, response, modules) {
    var userId = request.body.userId;
    var name = request.body.name;
    var portraitUri = request.body.portraitUri;
    var appKey = "";
    var appSecret = "";
    var random = Math.ceil(Math.random()*10000);
    var timestamp = Date.now();
    var before = appSecret + random + timestamp;    
    var signature = modules.oCrypto.createHash('sha1').update(before).digest('hex'); 
    var http = modules.oHttp;
    var bodyStr = "userId=" + userId + "&name=" + name + "&portraitUri=" + portraitUri;
    var options = {
        "url": "http://api.cn.ronghub.com/user/getToken.json",
        "headers": {
            'app-key': appKey,
            'content-type': 'application/x-www-form-urlencoded',
            'nonce': random,
            'signature': signature,
            'timestamp': timestamp
        },
         "body":bodyStr
    };
    http.post(options,function(err,res,body){
        response.send(body);
    })
}                                                                                                                                             	
```

---
** 如何联系Bmob技术和商务 **  
技术客服QQ：[2093289624](http://wpa.qq.com/msgrdv=3&uin=2093289624&site=qq&menu=yes)  
商务QQ：[2499654572](http://wpa.qq.com/msgrdv=3&uin=2499654572&site=qq&menu=yes)  
商务合作邮件：partner@bmob.cn  
技术沙龙邮件：event@bmob.cn

## Web开发者后台相关问题

** 如何在Web后台上传文件 **  
Bmob提供了一种非常简单的文件上传的方法：  

1.在Web后台中点击进入应用程序的控制面板中，如下图所示，选择需要用到文件的表，然后点击“添加一列”按钮，这时，弹出一个“添加新的表字段”的对话框。在这个对话框中，请输入字段名称，选择字段类型（**注意：请选择File类型**）。

![](image/addfile_1.png)

2.现在，你就可以快速上传文件了：点击“添加一行”按钮，在File字段中点击“Upload File”就可以直接上传文件。如下图所示。如果想要上传更多的文件，可以重复第二步操作。

![](image/addfile_2.png)

---
** 为什么导入CSV数据之后是乱码 **  
请先将导入的数据编码转换为“UTF-8无BOM格式编码”之后再上传（转换为UTF-8编码的一个简单方法是：用[Notepad++](http://notepad-plus-plus.org/)打开要导入的CSV文件，然后点击“格式->以UTF-8无BOM格式编码”菜单）。

---
** 为什么导出的CSV数据显示乱码 **  
导出的文件请以“UTF-8无BOM格式编码”格式打开查看(可使用[Notepad++](http://notepad-plus-plus.org/)打开CSV文件，然后点击“格式->以UTF-8无BOM格式编码”菜单)，如果用excel直接打开可能出现中文乱码！

---
** 能提供一个CSV文件参考下吗 **  
[点击这里下载CSV文件模版](http://static.bmob.cn/new/developmentdoc/appdemo/bmobtest.csv)  

使用方法：Web后台->创建应用->创建表->导入数据->选择这个CSV文件

---
** 能直接在Web后台上传文件吗 **  
可以，先在表中创建需要File类型的字段，然后新增一条记录就可以直接在Web端上传文件了。

---
** 导出数据表中的数据时可以自定义字段吗 **  
可以的。开发者后台->数据浏览->更多->导出数据，可以选择导出需要的列。  
![](image/export.png)

---
** 能通过在控制台添加Relation的数据吗 **  
可以，你可以点击relation字段，进去之后添加数据

---
** 如何获取_User表中的password **  
Bmob没有提供直接获取密码的方法。如果直接可以获取密码的话，会存在安全隐患的。如果非要这样做，你可以新增一个字段，记录明文的密码。

---
** Bmob中支持的String最大容量是多少 **  
4M

---
** 能不能设置主键 **  
可以，存在重复值会留下最早创建的记录，其它的删除。  
![](image/primarykey.png)

---
** 创建了数据库，可以在后台直接添加数据吗  **
可以

---
** 我想在eclipse用Java web开发，使用struts2框架，然后后台数据库用bmob可以实现吗，需要下载什么东西 **  
可以使用java sdk或者自己封装，通过https调用restful接口

---
** web端上传文件最大支持多少 **  
控制台上传的文件最大为50M

---
** 新建一张表添加字段为Relation，只能重新添加数据吗 **  
Web操作是这样的，但你可以用SDK，通过代码来实现数据的关联。

---
** 后台能不能支持批量上传文件？ **  
不支持，可以自己编写脚本完成。

---
** http请求如何访问Bmob **  
可以使用restful接口进行访问。

---
** ie8下引用 bmob-min.js 出现 “缺少标识符、字符串或数字” 错误 **  
ie8不支持html5

---
** angularJS如何与bmob配合使用 **  
可以使用我们的JS SDK或者是使用angularJS的网络请求使用restful接口进行请求

---
** 登录问题 能否实现只有通过验证的用户才能登 **  
登陆成功之后，你再获取当前的登陆信息，判断这个verified字段是否为true，这样就可以实现你的想法了。

---
** Bmob可以做微信公众平台的数据后台么 **  
可以

---
** 数据导出不带objectid 字段吗 **  
这个问题我们持续跟进，因为我们无法保证objectId不被用户修改，所以大家开发的时候就没有支持导出objectId了，之后看看怎么解决这个问题。

---
** 请问服务器上的表名和列名可以修改吗？ **  
不能修改，考虑发布后的APP会由于修改表名和列名而造成无法使用的问题。开发过程中可以通过删除再创建达到目的。

---
** 可以在PC端写tool来操作服务器数据? **  
可以，使用restful接口

---
** API请求数是实时统计更新的吗？ **  
不是的，API请求数一天统计一次，每天凌晨3点进行统计。

## APP官网相关问题

** APP官网的一些案例 **  
[http://bikenavi.bmob.site/](http://bikenavi.bmob.site/)  
[http://drive.bmob.site/](http://drive.bmob.site/)  
[http://qlslylq.bmob.site/](http://qlslylq.bmob.site/)

---
** 不使用SDK也可以创建APP官网吗 **  
是的。APP官网是我们为开发者提供的扩展服务，与SDK、云数据库、文件服务等其他业务没有任何联系，完全是耦合的关系。
使用APP官网的流程如下：注册进入官网->创建应用->点击“应用官网”->输入你想要的域名->选择模版->编辑保存。

---
** 官网修改后怎么没有立即生效 **  
我们采用生成静态文件的方式，生成和同步到泛域名服务器需要30秒的时间，请耐心等待。

---
** 能使用其他域名吗 **  
可以。但需要提交一些材料给我们（具体材料需要先联系我们的客服QQ），提交到工信部进行备案。

---
** 怎么知道我的域名是否备案 **  
登录网站 [http://www.miitbeian.gov.cn/publish/query/indexFirst.action ](http://www.miitbeian.gov.cn/publish/query/indexFirst.action ) 按操作查询即可

## 数据服务常见问题

** Bmob怎么设计赞和踩功能？ **  
利用原子计数器  
很多应用可能会有计数器功能的需求，比如文章点赞的功能，如果大量用户并发操作，用普通的更新方法操作的话，会存在数据不一致的情况。
详情请查看对应平台的原子计数器章节。

---
** 支持同步数据上传吗 **  
不支持阻塞主线程同步上传数据的方法！

---
** SDK请求时占用内存大吗 **  
如果只是数据服务的话，占用内存非常小。如果涉及图片服务，需要视图片大小而定内存占用情况。

---
** 文件能不能使用批量操作 **  
可以

---
** 查询单条数据的时候，只能通过objectId来查询么？ **  
如果确定是只有一个的，条件查询也可以。

---
** 注册和登录的流程是怎样开发的 **  
注册成功之后，服务器会返回`sessionToken`（标识用户登录成功的会话信息）给`BmobUser`对象，这时即可立即显示登录后台的界面，同步在后台调用登录接口进行登录操作。

---
** 登录踢人、改密码踢人相关 **  
一处登录其他地方下线以及改密码的问题请看如下伪代码：  
![](image/14669969347495.jpg)


---
** Bmob数据库的pointer和我自己使用外建字段的区别？ **  
pointer的好处是可以在查询的时候一并把关联的记录也查询下来，不需要二次查询。让查询的速度更快

### Android平台

#### 对象
** 为什么我修改表中的某个Number类型的字段，其他Number类型的都变为0呢？ **  
继承自BmobObject的类不要用int类型，用Integer。

---
** 定义类名必须和表中的名一致？ **  
类名和表名一致，表内字段名和类变量名一致。

---
** 插入一条数据之后怎么获得该数据的id **  
```
GameScore gameScore = new GameScore();
//注意：不能调用gameScore.setObjectId("")方法
gameScore.setPlayerName("比目");
gameScore.setScore(89);
gameScore.setIsPay(false);
gameScore.save(mContext, new SaveListener() {

@Override
public void onSuccess() {
    toast("添加数据成功，返回objectId为："+gameScore.getObjectId() + ”,数据在服务端的创建时间为：“ + gameScore.getCreatedAt());
}

@Override
public void onFailure(int code, String arg0) {
    // 添加失败
}
});
```
请看代码，成功后gameScore使用getObjectId()就可以获取objectId了。


---
** success方法中获取的数据，用全局变量接收，但是在方法外就接受不到，变量为空 **  
请先理解同步和异步的概念，回调中的onsuccess是异步方法，是不能用全局变量接收的，可以直接在onsuccess方法中做ui层面的更新

---
** 缓存路径能指定吗？ **  
不可以

---
** 我在User表中增加了一个Number类型的字段，设置为以1自增，但几天过去了，里面的值并未自动增加，这个自增是怎样自增的，还要去哪里设置吗？ **  
添加字段的时候选择num类型，有一个自增的checkbox和初始值的input，填一下就可以了

---
** 场景是多个客户端共同操作同一个数据表，更新该表的一个字段的值，如何做到一个客户端更新时锁定该数据表，操作结束时解锁？ **  
目前没有该功能，只有Number类型可以使用原子计算器达到该效果

---
** 一次查询多条数据 算是调用了几次API？ **  
一次调用算一次

---

** 请问每条数据的objectId都是唯一的吗，我的意思是，假设有个user表，有userName和level两个属性。如果两个对象的这两个属性都相同，其objectId是否就相同？ **   
objectId是每一条数据的唯一标示，不会出现重复的。

---

** String 数据类型最大可支持多大数据？ **  
最大为16M

---

** 求问怎么获取上传数据后生成的objectid  **  
保存数据成功后，你的BmobObject对象就有objectId了的。
或者你按条件查询得到的数据对象中也是包含objectId的。

---

** 数据查询必须要objectId吗？在用户数据表中，在无法获取用户objectId的情况下，如何查询一个用户是否存在，是否可以通过其他字段查询？ **  
单条查询必须使用ObjectId，多条查询时可以添加条件来进行查询。

---

#### 查询

** 查询成功，但是list只能在onSuccess方法中使用,如何在本类中的其他地方使用？ **  
网路请求都是异步独立线程的，你用`handler`把数据传递出来就可以。

---

** 如果不知道objectId，是否可以通过表中的元素获得数据？ **  
添加数据的时候，`onSuccess`中可以得到objectId。也可以通过条件查询得到对应的objectId的。

---

** 在Activity关闭的时候如何动态关闭查询？ **  
查询都是一次性的，并不需要取消

---
** bmob怎么查询一列数据并合并相同数据？ **  
可以使用统计查询中的groupby

---

** bmob的数据库操作方法save insert这些都有开线程吗  **  
bmob sdk提供的操作都是在线程中运行的，对外都是提供异步的回调方法，其回调方法，比如onsuccess和onFailure等是可以再UI线程中运行的，开发者不需要额外再开线程。

---

** Bmob查询数据结束标志 **  
在查询的回调方法中的onSuccess或onFailure触发时都是代表这个查询结束。

---
** Bmob能否进行多表查询？ **  
无法用一条语句查多张表，只能单独一个一个查

---

** 怎么设置缓存 让缓存数据在listView显示 **  
可以使用缓存查询，具体可以查看官方文档

---

** 怎么通过BmobUser的一个属性列来获取其他列的信息 **  
使用bmob的查询功能，查询Username 等于名称的用户信息即可，使用的是addWhereEqualTo方法

---

** 我的应用想只查询最新上传的一组数据，请问该如何操作呢 **  
可以根据时间来设置条件，再进行查询

---

** 查询中findListener中的onerror方法不执行,两次测试均是数据库无该数据的，但是程序均不执行onerror方法 **  
没有数据不代表查询出错，当没有数据符合你的查询条件时，就会返回空，此时还是执行onSuccess的

---

** 想问问查询的时候排序有多个关键字怎么解决？ **  
数据服务的文档中有的，在开发文档的查询数据->查询条件->排序那里： **  

排序

对应数据的排序，如数字或字符串，你可以使用升序或降序的方式来控制查询数据的结果顺序：

// 根据score字段升序显示数据
query.order("score");
// 根据score字段降序显示数据
query.order("-score");
// 多个排序字段可以用（，）号分隔
query.order("-score,createdAt");
说明：多个字段排序时，先按第一个字段进行排序，再按第二个字段进行排序，依次进行。

---

#### 数据关联

** 我有个Relation字段，想用它来记录喜欢这篇文章的用户，我该怎么添加里面的数据呢？ **  
这个问题请看 [数据关联](http://doc.bmob.cn/data/android/develop_doc/) 相关文档。

---

** Relation字段 能否像pointer一样在查询的时候一并把关联的记录也查询下来，不需要二次查询 **  
目前并没有这个功能，建议使用pointer

---

** activity是一个表，里面有一个BmobPointer org指向BmobUser，activity.getOrg.getObjectId总是为空呢？ **  
查询的时候应该没有用includ查询进去

---

** 查询数据时，表中的一个字段是pointer字段，如何将这个pointer字段的一个属性作为查询匹配条件？ **  
```
BmobQuery<Comment> query = new BmobQuery<Comment>();
BmobQuery<Post> innerQuery = new BmobQuery<Post>();
innerQuery.addWhereExists("image", true);
// 第一个参数为评论表中的帖子字段名post
// 第二个参数为Post字段的表名，也可以直接用"Post"字符串的形式
// 第三个参数为内部查询条件
query.addWhereMatchesQuery("post", "Post", innerQuery);
query.findObjects(this, new FindListener<Comment>() {
@Override
public void onSuccess(List<Comment> object) {
    // TODO Auto-generated method stub
    toast("查询成功:");
}
@Override
public void onError(int code, String msg) {
    // TODO Auto-generated method stub
    toast("查询失败:"+msg);
}
});
```
如上，就是使用内部查询就可以实现你的需求了，只需要将查询条件和表名换成你需要的就可以了～

---

** 如果一个用户要收藏一个产品应该怎么定义对象 **  
可以使用pointer类型

---

** 删除关联关系 **  
我现在有评论类如下：
```
public class Comment extends BmobObject {
private String comment;
private Found found;
private Lost lost;
private MyUser user;
}
```
如果我想删除Lost类或者Found类的某条数据  
其对应的Comment会被同时删除吗？  
如果不能应该怎么实现同时删除？  
不能同时删除，对于不同数据表的数据只能分别执行删除操作。

---

** 查询时 include 两个Pointer字段后会把前一个的数据冲掉
对表 AaaaEntity 查询时 include 两个Pointer字段后会把前一个的数据冲掉,如:
```
bmobQuery.include("userAuthor");
bmobQuery.include("xxxxEntity");

则:
aaaaEntity.getUserAuthor.getName()返回空

如果去掉后一行
bmobQuery.include("userAuthor");
//bmobQuery.include("xxxxEntity");
或
移到后面：
bmobQuery.include("xxxxEntity");
bmobQuery.include("userAuthor");

aaaaEntity.getUserAuthor.getName() 就能正常返回值
```

include的用法在文档里面已经说明了的(http://doc.bmob.cn/data/android/develop_doc/),想include多个就这样用：query.include("x1,x2");

---

#### 用户管理

** 打开了邮箱验证功能，注册成功后未验证也能登录成功？ **  
Bmob SDK中，邮箱的验证和用户的注册登录是异步的关系，也就是说，即使用户没有点击邮箱验证功能，也是一样可以登录成功的。如果需要限制用户的登录或者只能查看到登录后的部分功能，可以使用`BmobUser.getEmailVerified`。

---

** Bmob如何实现用户登录之后获取数据读写权限，以及如何实现登出操作的？ **  
用户登录之后，我们会把获取到的用户信息保存在本地文件中，你可以通过`BmobUser.getCurrentUser`方法获取对应的值，当调用 `logout`方法之后，这些缓存的数据就会清除。如果不调用`logout`方法，下次重新打开这个应用，还是可以通过`BmobUser.getCurrentUser`方法获得上次登陆的用户信息，从而判断是否登陆过。

---

** 清除缓存用户对象只是对本地清除，没有真正向服务端注销登录的账号，请问是怎么去处理这个问题 **  
BmobSDK中的BmobUser登录，只是登录成功后缓存用户信息到本地。服务端并没有记录用户的登录状态，所以退出登录并不需要向服务器注销。

---

** Bmob支持第三方登录吗？怎么做？ **  
支持，官方的文档上有介绍。


---

** 为什么邮箱验证还没去验证却可以登录 **  
是可以的，邮箱验证那个字段需要开发者根据需求自行决定要不要使用

---

** 登录时异常退出MyUser declares multiple JSON fields named mobilePhoneNumber **  
MyUser定义了一个Bmob的系统字段呀，你可以看看用户管理那里的文档，里面有介绍说明BmobUser的特有属性，以下摘抄自文档：  

BmobUser除了从BmobObject继承的属性外，还有几个特定的属性：  
username: 用户的用户名（必需）。  
password: 用户的密码（必需）。  
email: 用户的电子邮件地址（可选）。  
emailVerified:邮箱认证状态（可选）。  
mobilePhoneNumber：手机号码（可选）。  
mobilePhoneNumberVerified：手机号码的认证状态（可选）。

---

** 第三方登录之后该怎么获得User的objectId呢？ **  
登陆成功之后，系统就会给你生成一个objectId的，你正常的通过 user.getObjectId() 就可以得到了

---

** 如何修改user表中其他用户的数据 **  
直接在web控制台修改或者使用masterkey

---

** 修改数据提示User cannot be altered without sessionToken Error. **  
这种情况一般都是没有进行用户登录就对用户信息进行更新导致的

---

** 更新用户update时失败，9012错误 **  
9012是context is null,没传上下文对象

---

** 用了getobjectId方法为什么还是显示objectId cant't be empty。 **  
```
public void setsj(View v){
final User setUser = new User();
List<String> a=new ArrayList<String>();
a.add("5cd431f659");
a.add("4c2184e8ea");
setUser.setFriends(a);
setUser.update(this, setUser.getObjectId(), new UpdateListener() {

    @Override
    public void onSuccess() {
        // TODO Auto-generated method stub
        Log.i("bmob", "更新成功：");
        toast("更新成功");
    }

    @Override
    public void onFailure(int code, String msg) {
        // TODO Auto-generated method stub
        Log.i("bmob","更新失败："+msg);
        toast("更新失败");
    }
});
}
// 这段代码是通过点击一个button然后更新我写好的数据，可一直显示更新失败，查看logcat显示objectId cant't be empty。可是我有用setUser.getObjectId()啊，为什么还是说ID为空？
```
你的user并不是通过登录得到的，而是自己生成的，并没有objectid，需要从服务器上获取的数据才有objectid

---

** 更新了用户信息后 服务器都更新了数据 但是本地缓存用户没有更新 **  
更新用户信息后需要从新登陆，本地用户信息才会更新。

---

** 登录后在个人资料中上传头像在用户表，并且要头像和用户要对应。 **  
上传图片成功后，将BmobFile对象更新到当前用户的头像字段中即可。

---

** 在数据下_User 下把email添加后为啥 emailVerified Boolean 这一栏显示的是false 是什么原因呢 **  
该字段需要注册用户点击了验证邮件才会主动设置为true

---

#### 数据实时功能

** 如何实现Bmob服务端向Android应用发送实时通知？如某个数据过高需要提醒APP用户 **  
以使用实时数据监听功能来实现

---

** 登录之后，怎么获取用户的信息并显示出来 **  
登录成功之后就可以通过getCurrentUser方法获取本地用户信息

---

#### ACL和角色

** 例如我已经有一个角色叫Chief，我怎么用代码给它添加成员？直接new BmobRole("Chief")然后再getUsers().add然后再save?
但这个代码不应该是新建一个角色吗？如果是用BmobQuery<BmobRole>获取的话获取失败，返回101错误 **  
A:

```
//创建HR和Cashier两个用户角色（这里为了举例BmobRole的使用，将这段代码写在这里，正常情况下放在员工管理界面会更合适）
BmobRole hr = new BmobRole("HR");
BmobRole cashier = new BmobRole("Cashier");

//将hr_zhang和hr_luo归属到hr角色中
hr.getUsers().add(hr_zhang);
hr.getUsers().add(hr_luo);
//保存到云端角色表中（web端可以查看Role表）
hr.save(this); 

//将cashier_xie归属到cashier角色中
cashier.getUsers().add(cashier_xie);
//保存到云端角色表中（web端可以查看Role表）
cashier.save(this);
```

---

** 是否可以针一行数据的某一个字段控制读写权限 ？ **  
是否可以针一行数据的某一个字段控制读写权限 ？例如，UserA 发了一条说说，这条说说只有UserA可以写，其它用户可以读，但是其中有一个点赞计数字段，所有用户都可以对这条说说点赞，点赞后，这个点赞计数字段值就加1。 **  
没有针对一个字段控制读写的，如果需要，可以将这些需要控制的另外建一个表，使用pointer字段指向该表来获取

---

#### 地理位置

** 基于地理位置的查询是根据什么排序的 **  
是按照距离从近到远来进行排序的

---

#### 自动更新

** 自动更新生成的表和文档上的不一致 **  
没有调用initAppversion方法

---

** 自动更新，如何实现只获取是否有新版本，不弹出对话框。 **  
目前SDK中暂没有这个功能，后续版本会考虑添加

---

#### 文件

** Bmob如何实现储存和传输图片？ **  
通过`BmobFile`类上传图片，上传成功之后，会返回一个`BmobFile`，你从这个`BmobFile`可以得到文件上传之后的url，把这个url保存到你的对应表中。下载的时候，先查询数据表得到url，然后下载这个图片就可以了。 

---

** Bmob如何将整批图片下载在本地呢？ **  
首先先查询，得到全部数据，从而得到图片的url列表，再用一些下载文件的代码把图片批量下载下来。

---

** BmobFile类最多可以保存多少张图片？ **  
`BmobFile`类只能保存一张图片，你可以用`BmobFile`上传图片，得到图片的url，保存的字段用string或者array。

---

** 怎么让表的某个字段包含多张图片？ **  
用array来存储文件的url

---

** 能把json文件放在bmob里，并配置一个专门的地址，然后APP通过这路径下载或者读取吗？ **  
用文件服务实现即可。

---

** 怎么通过objectID获得文件的下载路径？ **  
```
// 根据objectId查询数据
BmobQuery<GameScore> query = new BmobQuery<GameScore>();
query.getObject(this, "a203eba875", new GetListener<GameScore>() {

@Override
public void onSuccess(GameScore object) {
// TODO Auto-generated method stub
toast("查询成功：");
//获得playerName的信息
object.getPlayerName();
//获得数据的objectId信息
object.getObjectId();
//获得createdAt数据创建时间（注意是：createdAt，不是createAt）
object.getCreatedAt();

// 假设GameScore对象中有一列是BmobFile类型的icon
// 如下取出查询到的数据中的BmobFile类型，得到下载地址
BmobFile icon = object.getIcon();
String url = icon.getFileUrl();

}

@Override
public void onFailure(int code, String arg0) {
// TODO Auto-generated method stub
toast("查询失败："+arg0);
}

});

```

---

** 为什么最新的SDK里面的BmobFile没有loadImageThumbnail方法 **  
最新的SDK已经将图像处理的接口去掉了，需要用户自己在本地处理


---

** 怎么去在批量上完图片之后，取得对应的缩略图呢？ **  
缩略图功能已经取消，请在客户端进行图片的处理

---

** 9015your uploading task is canceled. 安卓文件上传无响应 **  
调用了bmobfile.cancel()方法会出错该提示。

---

** 表中有一列数据为BmobFile类型 ，数据为.TXT格式 ，怎么将文件下载下来 **  
查询这一行数据，在结果中从这一列对应的BmobFile对象中用getFileUrl()得到文件的地址，再进行下载。

---
** listview显示Bmob上的图片怎么实现？ **  
图片上传后会返回相应url给客户端的，可以在表中，在需要显示的时候利用url将图片下载下来进行显示

---

** 我通过软件上传了文件到bmob后端云。怎么获得该文件url。 **  
上传后会有url返回

---
** bmob可以通过客户端下载文件吗？ **  
上传到Bmob之后就会返回文件的地址，至于怎么下载，由你来决定。

---
** 为什么我上传的文件(图片)已经删除了，但是通过url仍然可以访问到图片呢？ **  
CDN缓存的，过一段时间就会完全删除

---

#### 其它问题

** Cause: com.android.dex.DexException: Multiple dex files define Landroid/support/v4/accessibilityservice/AccessibilityServiceInfoCompat$AccessibilityServiceInfoVersionImpl;
Error:Execution failed for task ':app:transformClassesWithDexForDebug'. **  
Cause: com.android.dex.DexException: Multiple dex files define Landroid/support/v4/accessibilityservice/AccessibilityServiceInfoCompat$AccessibilityServiceInfoVersionImpl;
Error:Execution failed for task ':app:transformClassesWithDexForDebug'.  
这是重复导包造成的，你用的v4和v7包重复了，你需要去掉报错的那个模块

---

** 我使用BmobUser.login接口,返回onFailure的参数code分别对应什么情况?有说明文档么? **  
[错误码列表](http://doc.bmob.cn/other/error_code/)

---

** App_ID is not setted出现什么原因？ **  
初始化BmobSDK时需要传入你自己应用的ApplicationID

---

** Duplicate files copied in APK META-INF/maven/com.squareup.okhttp/okhttp/pom.xml **  
导了重复的包

---

** bomb_AndroidSDK_V3.4.7_0518 中文乱码 **  
SDK的demo的编码格式是gbk,换下格式就行

---

** android Bmobquery 开两个线程 分别查两个不一样的表，返回数据有问题 **  
sdk中的很多方法本身就是在子线程中执行的，开发者没必要开子线程(创建子线程和线程池管理SDK都封装好了)。

---

** 查询出了回调函数，List就变空了 **  
请先理解下同步和异步的概念，bmob目前的接口提供的都是异步回调函数，建议在onsucess/onFailure中进行ui操作

---

** Bmob的各个SDK可以使用Application的Context来初始化吗 **  
可以的。最好是用Application的Context来初始化。

---

** bmob的jar包和volley包冲突怎么回事 **  
bmob的jar里面包含了volley,无需再次导入

---

** 移动端和WEB端能用BMOB作为云端，实现数据共享么？ **  
可以的，使用同一个app id来进行操作即可

---

** 真机运行时控制台输出 Error:warning: Ignoring InnerClasses attribute for an anonymous inner class **  
可以试试在你的app的build.gradle的android标签下添加如下：
```
lintOptions {
ignoreWarnings true
}
```

---

** 把应用装到手机很慢，一直在Gradle Build **  
如果你确定你的应用所需的jar包已经下载完了，可以将gradle设置成离线模式

---

** BmobSDK能导入源码开发编译吗 **  
BmobSDK目前并未开源

---

** 3.4.7 sdk java.lang.UnsatisfiedLinkError 怎么破  
java.lang.UnsatisfiedLinkError: Couldn't load bmob from loader dalvik.system.PathClassLoader[DexPathList[[zip file "/data/app/top.kiuber.sharemy-1.apk"],nativeLibraryDirectories=[/data/app-lib/top.kiuber.sharemy-1, /vendor/lib, /system/lib]]]: findLibrary returned null **  
详情移步到博客http://www.kiuber.top/2016/05/24/android-studio-add-so/  
问题已经被攻克，原因是so库文件未导入。  
解决方法：在project视图下，在main文件夹内新建jniLibs文件夹，把对应so库文件夹及文件复制到jniLibs文件内，然后在MainActivity.java文件

---

** 邮箱验证用哪个SDK  **  
使用数据服务SDK即可

---

** Android studio连接Bmob时报错 **  
```
java.lang.UnsatisfiedLinkError: com.android.tools.fd.runtime.IncrementalClassLoader$DelegateClassLoader[DexPathList[[dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-support-annotations-23.4.0_eff36cb3dd5776bcc7dfe63d3c4af3d7d0b02909-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_9-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_8-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_7-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_6-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_5-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_4-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_3-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_2-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_1-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-slice_0-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-okio-1.7.0_16f89fb230458d29c309937f6ab11ce75258c504-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-okhttp-3.2.0_8f755226a0726d7921fa90d83c674c16a1bd0ee3-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-internal_impl-23.4.0_2c4831db21059d6465959fb999a28d5a6fe10599-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-com.android.support-support-vector-drawable-23.4.0_eb28b4ae1a0615e1130648d3b547db30e6e89fd0-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-com.android.support-support-v4-23.4.0_c594c96eba293bbb78cda22a0502566240fb4409-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-com.android.support-appcompat-v7-23.4.0_39e8b9d21669eb9eb3df764bcd49eb0facc75e07-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-com.android.support-animated-vector-drawable-23.4.0_613291d2784b41eebf3800d518847e90b2efa55b-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-bmob-sdk-3.4.7_3bb8e20fe85419a97fea506c0c8a8a8fe18f45d5-classes.dex", dex file "/data/data/com.example.administrator.bmob2/files/instant-run/dex/slice-bmob-push-0.9_35e71e7e49d7888481221634e134fec14816f381-classes.dex"],nativeLibraryDirectories=[/data/app/com.example.administrator.bmob2-2/lib/arm, /vendor/lib, /system/lib]]] couldn't find "libbmob.so
```
使用aar格式的SDK，这样就不用导入so库

---
** sdk怎么和Retrofit这些库一起使用呢 **  
出现这个问题的原因是retrofit依赖的okhttp和sdk的远程aar包中的okhttp重复导致的，将会导致编译不过，解决方式有：  
1 下载Retrofit的jar包，采用本地依赖的方式；  
2 compile Retrofit的配置加下exclude，把重复的okhttp除去，如下：  
```
compile ('com.squareup.retrofit2:retrofit:2.1.0'){
        exclude group : 'com.squareup.okhttp3'
    }
```

### iOS平台

#### 对象

** 查询表内容时不能获取到objectId的值，通过[obj objectForKey:@"objectId"]获取到的是空值，其他字段是正常的 **  
BmobObject有一些基本属性，objectId，createdAt，updatedAt等，直接获取就可以了,如bmobObject.objectId。

---

** 查询时可以设置只从本地缓存获取，但是创建和保存时是否能够只保存到本地缓存呢？ **  
只有查询有缓存，其它操作没有缓存。

---

** iOS 怎么获取到创建日期啊 **  
NSLog(@"%@",[NSString stringWithFormat:@"%@", Myobject.createdAt]);

---

** bmob 怎样用代码写唯一键  **  
唯一键只能在控制台设置

---
** 我的bmob对象中有一个属性是boolean属性，请问在ios代码中怎么设置它？ **  
BOOL cheatMode = [[object objectForKey:@"cheatMode"] boolValue];
isStudent = [NSNumber numberWithBool:NO];
用以上的方法来设置。

---

** ios开发初始化一个对象指定一个id但是保存成功之后却不再是这个id了 **  
objectId系统生成的，并不是你来生成的，你用的下面这个方法，是用来构造已经存在的对象，然后对该对象进行更新删除操作的。
```
BmobObject *gameScore = [BmobObject objectWithoutDatatWithClassName:@"GameScore" objectId:@"a"]；
```

---

** 原子计数器怎么用 **  
查看[开发文档](http://doc.bmob.cn/data/ios/develop_doc/)原子计算器小节。

---

** 在iOS中 在代码中如何创建一个空表 只包含各列的属性 而不创建具体的一条数据。 **  
该需求无法可以通过在web控制台添加列来实现。

---

** 如何删除表中所有的数据？(只知道表名的情况下) **  
先查询该表所以数据，获得数据后遍历删除～

--- 

** 可不可以批量创建数据 **  
可以。请查看[开发文档](http://doc.bmob.cn/data/ios/develop_doc/)批量数据操作小节

---

** 如何存储比较复杂的数据类型？比如数组里包含字典，字典里再包含数据 **  
一般的数据类型使用使用JSON格式都可以存储的，可以多了解一下JSON格式

---

** 'Invalid type in JSON write (CLPlacemark)' CLPlacemark类型熟悉无法写入 **  
对象类型属性是无法写入的

---

#### 查询

** iOS端集成 查询单条数据，只知道某个value的具体值，如何查询相应的该条数据的其他值？ **  
使用多条查询并加上你的约束条件就可以了

---

** iOS 查询条件是boolean 应该怎样设置？ **  
类似于以下形式
```
[bquery whereKey:@"playerName" notEqualTo:[NSNumber numberWithBool:NO]];
```

---

** 我想让模糊查询的条件key为所关联的_User表中的username 怎么弄 **  
你好，文档中有关于模糊查询的介绍[查询](http://doc.bmob.cn/data/ios/develop_doc/)

---

** BmobQuery查询多条数据时，查询结果无法传出 **  
查询是异步的，可以采用通知机制来传递返回的数据，或者是把操作逻辑放在block里

---

** user表查询返回的没有自定义列的数据，只有username自带属性 **  
注意使用objectForKey来读取数据，而不是valueForKey。

---

** iOS 如何判断表内存在某列存在某项值 然后作为类方法返回值返回呢？ **  
查看以下文档中的“列值是否存在”小节[开发文档](http://doc.bmob.cn/data/ios/develop_doc/)

---
** 支持一次可以查找多张结构类似的表吗 **  
不支持

---

#### 数组

** IOS 如何 查询 数组 **  
 

```
BmobQuery   *bquery = [BmobQuery queryWithClassName:@"GameScore"];
//查找GameScore表所有数据
[bquery findObjectsInBackgroundWithBlock:^(NSArray *array, NSError *error) {
    for (BmobObject *obj in array) {
        //打印array
        NSLog(@"obj.array = %@", [obj objectForKey:@"array"]);
}
}];
```

---

** 删除array数据类型的一个元素 **  
[开发文档](http://doc.bmob.cn/data/ios/develop_doc/)数组小节

---

#### 数据关联


** 怎么获取relation中的数据?  **  
假设你有一个帖子(Post)类和一个系统默认的用户(User)类, 而每一个帖子(Post)都可以被不同的用户(User)所喜欢。 如果帖子(Post)类下面有一个Key名为likes，且是 Relation 类型, 存储了喜欢这个帖子(Post)的用户(User)。那么你可以找到喜欢过同一个指定的帖子(Post)的所有用户：

	BmobQuery *bquery = [BmobQuery queryForUser];
	[bquery orderByDescending:@"updatedAt"];
	BmobObject *obj = [BmobObject objectWithoutDatatWithClassName:@"Post" objectId:@"a1419df47a"];
	[bquery whereObjectKey:@"likes" relatedTo:obj];
	[bquery findObjectsInBackgroundWithBlock:^(NSArray *array, NSError *error) {
	}];

---

** 如何查询多个关联关系 **  
如果查询多个关联关系，可以使用以下方法，使用逗号(,)操作来使查询中包含多个属性
```
[bquery includeKey:@"column1,column2,..."];
```
---

** iOS-如何判断列值Pointer类型里的数据不为空 **  
可以用下面的方法来实现～
```
//设置查询中该字段是有值的结果
-(void)whereKeyExists:(NSString *)key;
//设置查询中该字段是没有值的结果
-(void)whereKeyDoesNotExist:(NSString *)key;
```

---

** Relation关系，如何进行逆向查询？ **  
基于User可以点赞Post，我现在在Post表中建立了一个Relation关系，指向User；借此我可以知道，喜欢了某一篇Post的User都有谁。  
现在我还需要知道某一个User喜欢了哪些Post，也就是利用User的ObjectID查询Post表的内容。貌似Bmob的Relation关系与数据库里面的多对多关系（借用建立中间表实现多对多）不同，不知道该怎样实现我所要的查询？
这个没法直接逆向查询的，你可以使用pointer来完成你的需求，重新建立一个表，两个字段，一个指向点赞者，一个指向点赞人

---

** iOS中怎样同时查询两张表，做到获取两张表的内容，不是一张表的内容 **  
可以采用pointer类型，使得一张表指向另一张表，再使用include接口可以来获得

---

#### 用户管理

** 注册的时候如何给User表自定义的字段插值？ **  
有个`BmobUser`类用来操作用户相关的数据  
```
	BmobUser *bUser = [[BmobUser alloc] init];  
	[bUser setUserName:@"小明"];  
	[bUser setPassword:@"123456"];  
	//age 为自定义  
	[bUser setObject:@18 forKey:@"age"];  
	[bUser signUpInBackground];
```

---

** 打开了邮箱验证功能，注册成功后未验证也能登录成功？ **  
Bmob SDK中，邮箱的验证和用户的注册登录是异步的关系，也就是说，即使用户没有点击邮箱验证功能，也是一样可以登录成功的。如果需要限制用户的登录或者只能查看到登录后的部分功能，可以使用`[[[BmobUser getCurrentUser] objectForKey:@"emailVerified"] boolValue]`方法。

---

** Bomb邮箱认证是只需要开启邮箱认证就可以了吗？里面的内容要不要设置啊，比如发送给谁，邮箱地址什么的？ **  
开启就可以了使用了。内容可以不用设置，发送给谁、邮箱地址是什么是由SDK注册的时候用户填写的。

---
** ios注册的时候如何给User表自定义的字段插值 **  
有个BmobUser类用来操作用户相关的数据
```
BmobUser *bUser = [[BmobUser alloc] init];
[bUser setUserName:@"小明"];
[bUser setPassword:@"123456"];
//age 为自定义
[bUser setObject:@18 forKey:@"age"];
[bUser signUpInBackground];
```

---

** 第三方用户授权注册登录后，如何绑定手机号呢？ **  
可以使用该绑定手机号的功能，请查看[开发文档](http://doc.bmob.cn/data/ios/develop_doc/)手机号相关功能小节

---

** 退出登录接口 **  
[BmobUser logout];

---

** 手机号是用户名，在忘记密码这一块，用什么来方法来查询用户名？用什么回调方法去判断用户是否已经注册 **  
可以直接使用条件查询来判断是否已经存在该用户

---

** 用第三方登录时,怎么将用户头像存入BmobUser中 **  
再建一个字段，将头像url存进去

---

** 我做了两个页面（viewcontroller）,在注册页面用[BmobUser setUsername:]等方法保存了用户账号密码的信息，成功之后使用[BmobUser loginWithUsernameInBackground:,**]这个方法保存后台，但是我在另一个页面，登录页面提取数据进行账号密码对比验证的时候，使用[BmobUser getCurrentUser]提取当前的账号密码，发现他的账号内容保存了下来，而密码的内容是NULL。不知道这是为什么 **  
密码是不能提取的，登录要用文档给定的接口

---

** ios中 ，怎么判断用户注册或是登陆的时候 处于联网状态还是非联网状态 **  
可以使用网络状态监听，这方面的资料有很多的～http://www.cnblogs.com/wendingding/p/3950114.html

---

** 请问每次登录后都会缓存用户的信息，但是好像没有缓存密码，那怎么实现缓存登录，也就是下次自动登录。 **  
密码是不会保存的，启动应用时直接使用下面代码判断用户是否已经登录
```
BmobUser *bUser = [BmobUser getCurrentObject];
if (bUser) {
//进行操作
}else{
//对象为空时，可打开用户注册界面
}
密码是不会保存的，启动应用时直接使用下面代码判断用户是否已经登录
BmobUser *bUser = [BmobUser getCurrentObject];
if (bUser) {
//进行操作
}else{
//对象为空时，可打开用户注册界面
}
密码是不会保存的，启动应用时直接使用下面代码判断用户是否已经登录
BmobUser *bUser = [BmobUser getCurrentObject];
if (bUser) {
//进行操作
}else{
//对象为空时，可打开用户注册界面
}
```

---

#### 数据实时功能

** 客户端监控某个表或某一行数据，会使客户端电量或网络流量增加吗？如果表数据有变化时，是通过推送机制来通知客户端的吗？ **  
不会消耗多少网络流量的，是用websocket机制来通知客户端，不是通过推送，也没有离线消息的概念，一旦socket连接关闭，就不会收到后续消息。

---

#### ACL和角色

** 如果每个用户都有写入权限，安全应该怎么做？  **  
可以设置ACL，详情请查看文档[开发文档](http://doc.bmob.cn/data/ios/develop_doc/)ACL和角色小节

---


** ios安全问题，如果每个用户都有写入权限，安全应该怎么做？ **  
可以使用ACL来限制读写权限。

---

** 关于ACL安全控制的几个问题  
1.在后台设置了某个表的权限为只读，那么app上调用setPublicWriteAccess，是不是对该表无效？  
2.app上是否有acl的api改变表是只读还是acl控制？   
3.下面代码是不是对该应用中所有表进行acl权限设置？  
```
BmobACL *acl = [BmobACL ACL];
//设置所有人读权限为true
[acl setPublicReadAccess];
//设置所有人写权限为true
[acl setPublicWriteAccess];
```
如果只是对blog表权限设置，在上面的基础上加上blog.ACL= acl;即可？但是我觉得这样好像有点矛盾，因为如果前面的代码成立，那么后面的后面代码没有达到“只是对blog表”的权限修改的目标，反而到时所有表的权限都被修改了。  
4.setPublicWriteAccess是对所有表的权限设置，有没有只针对某个表所有行的权限设置的api？  
5.开发文档中的关于发表一篇不公开的日志的例子，我理解为是对表中都一条单独的数据进行acl权限控制，这种理解是否正确？  
6.ACL能不能控制某个字段（也就是列）的访问权限？ **  

1.调用应该是有效的，这个你只需要简单测试一下就可以了。  
2.除了只读后，其它情况都是acl控制。  
3.不是对所有表进行设置，那个代码只是设置了权限，必须显示对某个表应用才行。  
4.同3，并不是针对所有表进行设置。  
5.是的  
6.不能，只能控制表的访问。

---

#### 文件

** iOS上传文件只支持路径上传吗，不支持iOS的NSData或者image对象上传吗 **  
支持路径和NSData上传，可以查看BmobFile的头文件，里面有相关注释

---

** file字段中如何上传多张图片？ **  
一个file字段只能保存一个图片文件，多个图片可以使用数组将图片url保存下来

---

** File类型是视频文件，能不能在ios端直接通过File的地址播放视频呢？ **  
支持

---

** iOS 从相册获取到视频 然后如何上传 **  
直接通过路径或者NSData都可以

---

** 上传视频失败 **  
![](image/14661501969652.jpg)
这种情况是初始化没有完成就开始进行请求导致的，可以监听kBmobInitSuccessNotification通知，监听到该事件后再上传即可

---

** 在ipv6下.无法获取到资源文件 **  
先看看ipv6的环境是否设置正确[设置方法](https://developer.apple.com/library/mac/documentation/NetworkingInternetWeb/Conceptual/NetworkingOverview/UnderstandingandPreparingfortheIPv6Transition/UnderstandingandPreparingfortheIPv6Transition.html#//apple_ref/doc/uid/TP40010220-CH213-SW1),再看看相应的下载库是否支持ipv6。

---

** 1.69 SDK 文件服务更换为CDN上传是指什么？文档在哪里？ **  
原接口不变，只是服务器换了，服务会更稳定的

---

#### 地理位置

** 地理位置查询 返回的结果是已经排序的 **  
是排序好的，由近到远的顺序。

---

** 想查询10KM内的所有用户，并且按用户的某个字段属性排序，应该怎么做呢？因为发现只要按地理位置设置了条件，不管排序条件怎么设，最终都是按距离远近进行排序的... **  
做不了的，有地理位置条件的时候都是按从近到远排序的。距离相同再按别的排序

---

#### 其它问题

** 有iOS 点赞功能的demo吗？ **  
有的，[Bmob点赞案例](https://github.com/limaofuyuanzhang/BmobLikeDemo) 实现的用户注册、用户登录、发贴、显示所有帖子资料以及对帖子进行点赞的功能 。

---

** 请问有对应的swift开发方法吗？ **  
Swift项目中使用BmobSDK可以看这个文档：[Swift项目中使用BmobSDK](http://docs.bmob.cn/data/iOS/l_swift/doc/index.html)

---

** 支持什么编译器 **  
Bmob完全支持iOS 64bit/32bit的真机和模拟器调试。

---
** 数据库中file字段无法导出吗？ **  
暂时只支持7种基本类型的导出：字符串(String)、数字(Number)、布尔值(Boolean)、
数组（Array）、对象（Object）、日期（Date）和地理位置（GeoPoint）


---

** iOS开发restAPI中条件查询如何拼接请求 **  
写在url上面，可以先了解一下html中get和post的区别，get请求的参数都是写的url上的~

---

** bmob有iOS国际化文件没有 **  
国际化是需要你自己在本地做的，和Bmob无关。

---

** 出现错误"msg":"authorization has expired","code":40300006 **  
应用太久没有请求导致的，先在控制台恢复一下应用数据就可以

---

** 等到查询成功得到结果后再执行下一步怎么办？ **  
需要放在block中进行。

---

** 出现错误Error Domain=cn.bmob.www Code=20002 "connect failed!" UserInfo={NSLocalizedDescription=connect failed! **  
网络问题，连接失败了，请尝试更换网络再次进行连接。

---

** The dependency `BmobSDK` is not used in any concrete target. **  
你好，应该是你的cocoapod升级了，新版本的需要指定下载的库给特定的target使用，如下，把CocoapodsDemo换成你的target名即可～

```
target “CocoapodsDemo” do
pod ‘BmobSDK’
end
```

---

** 想迁移一个app的某个表数据到另一个app，怎么实现 **  
可以直接使用A应用的备份数据生成新应用提供给B应用使用，点击进入应用，设置-备份还原，选择最近一次备份生成新应用即可

---

** 怎样往一张表里面直接添加图片，不用代码 **  
web上传

---

** os 用户删除 tableView 某一个单元格的数据，我怎么拿到用户点击的 index.row 去找到该行数据相应的 objectId？ **  
显示的时候是把bmobobject放在一个数组中显示,直接根据row找到对应的bmobobject，里面就有objectid

---

** 错误Error Domain=cn.bmob.www Code=100 "db stopped" UserInfo={NSLocalizedDescription=db stopped} **  
应用可能太久没使用被停止了，到控制台对应的应用的设置那里恢复一下数据

---

** Cocoapod集成后打开报错，提示缺失库。 **  
打开后缀xcworkspace的文件，而不是后缀xcodeproj 的文件

---

** 哪里可以看到错误码 **  
[错误代码列表](http://doc.bmob.cn/other/error_code/)。

### Cocos2d-X

** BmobQuery查询 怎么查看返回的data？ **  
CCLOG("%s",(const char*)data);或者是BmobLog::bmob_log()

---
** 要添加头文件？ **  
![](image/14670192736563.jpg)
不是添加文件的问题，是你的SecondScene没有实现BmobSaveDelegate接口，你实现BmobSaveDelegate接口就好了．

---
** bmob中的cocos2d-x怎么不提供静态和动态库！而且里面还存在多种编码格式！请提供一下bmob coocs2d-x的动态库和静态库。或告知相信解决办法。 **  
目前暂不提供。


### CSharp

** 为什么我调用支付应用无论是支付宝还是微信点击都没有反应呢(请教一下unity接支付) **  
目前暂不支持Unity支持

---
** unity端 查询表，会出现失败情况 **  
失败原因 Failed to connect to api.bmob.cn port 443: Timed out, and response content is 
UnityEngine.MonoBehaviour:print(Object)  
提示连接超时，先检查一下网络状况。

---
** unity不能缓存用户吗？ **  
c#没有进行用户缓存

---
** Bmob能存放Unity的AssetBundle么 **  
可以使用文件上传来存储～

---
** 如何通过SDK删除用户表_User的数据 **  
可以通过调用restful接口+master key来完成删除用户

---
** C#SDK，使用Find功能，我自己封装一层查询的方法，想要获得bool的返回值，应该怎么实现 **  
不能返回，只能使用回调，因为Find方法是异步执行的．

---
** 请问在c#sdk可以使用master key吗？还是说要自己重新写？ **  
不可以直接使用的，只有Restful api可以使用master key，你可以使用C#的http请求api来调用restful api

---
** Bmob如何实现两张表的关联呢?   
比如我需要将User表与Role表进行关联，登录用户后，系统可以通过User的帐号来获取与之相应的Role表里面的信息？ **  
可以，用列的pointer或者relation类型，具体用法看文档

---
** Unity可以使用短信验证么，为什么找不到API **  
可以使用Unity的网络访问接口，调用restful来使用短信验证～

---
** bmob sdk for unity3D 在unity3d5.3 下转il2cpp无法使用  
用 unity3D 5.3 打il2cpp 转c++ 后会报错：  
Unsupported internal call for IL2CPP:DynamicMethod::create_dynamic_method - System.Reflection.Emit is not supported.  
应该c++静态代码是不支持 System.Reflection.Emit 的反射类，能有其他解决方法吗？ **  
这个目前还没有好的解决方法，JSON很多操作都用了反射～

---
** unity3d bomb sdk 打包到IOS上.请求返回缺少404里面的数据. **  
升级u3d版本至5.3.2f以上。

---
** 怎么做点赞的用户唯一性,要做点赞，可以用原子计数器，但是无法知道是哪个用户点的赞，而且每个用户只能最多加一个赞，用Array来存用户objectid可以，但是存在多用户同时点赞相互覆盖对方的objectid的情况，请问有什么办法可以解决吗？ **  
可以重新建立一张表，两个pointer字段一个指向点赞用户，一个指向被点赞的内容。
 
---

** 怎样把github上下载的unitysdk注入到unity project里面 **  
官网的文档比较老没有同步更新。直接看下案例（接下来把文档整理下）：  
https://github.com/bmob/bmob-demo-csharp/tree/master/examples/bmob-unity-demo
libs路径：  
https://github.com/bmob/bmob-demo-csharp/tree/master/examples/bmob-unity-demo/Assets/libs

---

** untiy 开发怎么集成周围的人功能,可以做这个功能吗 大概怎么个思路 有相关的文档吗？ **  
可以采用地理位置来实现，我们有现成的api返回一定范围内的用户记录。

---

** C# BmobRelation做粉丝和关注怎么做 **  
看RoleTest这个例子,https://github.com/bmob/BmobSharp/blob/master/BmobTest/BmobTask.cs

---

** unity5中，最新版的bmob什么地方可以输入Application ID？ **  
https://github.com/bmob/bmob-demo-csharp/tree/master/examples/bmob-unity-demo

---

** unity下，我如何传递参数到云端代码，然后获取云端运行后的回调呢？ **  
```
云端代码：
function onRequest(request, response, modules) {
var res = {"value": "just string..."} ;
response.end(JSON.stringify(res));
} 

C#调用代码：

[TestMethod()]
public void EndpointParamAndStringTest()
{
var p = new Dictionary<String, Object>();

var future = Bmob.EndpointTaskAsync<Object>("testString", p);
FinishedCallback(future.Result, null);
}

```

---

** bmob查询时记录返回值的表必须是自己新建的表吗？c#里不能用datatable吗？ **  
返回值都是你创建的表，不一定是新的。这样C#才能映射到对应的object中去，让你对象化调用。

---

** bmob使用指定列查询时会多出几种数据,分别是_type,，createdAt等。 **  
是的，这些是默认的系统列，一定要有的。

---

** 
1.unity里面必须使用BmobUnity Bmob = gameObject.GetComponent<BmobUnity>();  
来获取bmob对象吗 ？能不能 用C#DLL里面的 new方法呢？因为BmobUnity继承了mono所以不能new这个很麻烦，毕竟数据操作是模型层干的事情  
2.在查找数据的时候，Main.Bmob.Find方法不在主线程 ，也没有回调，导致后面的代码在结果出来之前优先执行了。  
3.以上两面我看c#的SDK完美解决了，可惜unity里面不能用c#的bmob.dll **  

1.不能用new的方式，bmob异步请求用了MonoBehaviour#StartCoroutine  
2.没有回调？？自己先查看下API。  
3.Unity和C#不同的，Unity是一个封装的版本，需要兼容各个平台的东西。


---

** C# sdk 只可以用Unity开发吗？visual c#可以用这SDK么？ **  
C# SDK可以用来开发Unity、visual c#，wp8这几类的程序。

---

** unity中调用restapi方法分享 **  
![](image/14673655321255.jpg)
![](image/14673657074024.jpg)


### JavaScript

** 请问比目有TypeScript的前端sdk吗？主要是用在白鹭游戏引擎引擎里的。 **  
这个暂时没有，有普通js的sdk

---

** angularJs如何与bmob配合使用 **  
一般这种情况需要将和Bmob的数据交互封装为一个service，从service中返回数据
基本的调用层次就是controller调用service，service调用Bmob
bmobservice.js

```
app.service("bmobservice", function () {
//添加一个资源  Bmob对象在index中初始化或者在app.run中进行初始化
this.AddResource =function(resource){
    var ResourceInfo = Bmob.Object.extend("ResourceInfo");

    //创建对象
    var resourceInfo = new ResourceInfo();
    //为对象赋值
    resourceInfo.set("Title",resource.Title);
    resourceInfo.set("ResourceType",resource.ResourceType);
    resourceInfo.set("Target",resource.Target);

    //resourceInfo.save();
    var array = new Array();
    var SubResourceInfo = Bmob.Object.extend("SubResourceInfo");
    var subResourceInfo = new SubResourceInfo();
    subResourceInfo.set("Name",resource.SubResourceInfo[0].Name);
    subResourceInfo.set("Url",resource.SubResourceInfo[0].Url);
    resourceInfo.set("SubResource",subResourceInfo);
    resourceInfo.save();
}
});

```

testcontroller.js

```
app.controller('testcontroller',function($scope,$resource,bmobservice){
        $scope.addresource = function(){
            var resource = {
                "Title":"test",
                "ResourceType":0,
                "Target":"test",
                "SubResourceInfo":[{
                    "Url":"testurl",
                    "Name":"testname"
                }]
            }
            bmobservice.AddResource(resource);
        }
```

---

** 没有客户端请求的情况下服务端能主动向客户端发送数据吗？ **  
不能

---

** 有没有比较数据表中内容相似度的方法,例如 我表里面有 一个组数据 name: 你好中国人， 我要往里面房数据但是如果我的数据为 name：中国人 ，就不放进去了。。判断两者为同一数据 **  
这种定制化的需求需要开发者自行实现。

---

** 有没有办法可以获取password **  
为安全考虑，我们不对外提供获取password字段值的功能。

---

** Javascript的bmob的数据处理都是异步的，如何设置为同步 **  
如果是在nodejs中，可使用async这个同步类库

---

** 如何在node.js的代码中调用bmob **  
用bmob的nodejs模块

---

** JS如果想产生多行数据保存到表中怎么办? **  
一次只能保存一条数据，多条数据需要使用批量操作，可以使用restful接口

---

** js sdk中有更新某个表某个字段所有值的函数吗 **  
没有的，只能一个个更新，restful有一个批量更新的接口，但是每次最多只能操作50条数据

---

** JavaScript 传输数据时，自动加密了吗？ **  
Bmob所有SDK的通讯过程都进行了加密。

---

** 消息推送 JS SDK支持吗？我使用H5进行APP开发 **  
JS有推送功能，可以查看推送文档。

---

** BmobSocketIo.onUpdateTable可以无视ACL **  
实时监听功能不受ACL的限制。

---

** JS SDK 的初始化语句应该放在哪里？ **  
用框架集成到一个页面，例如angularjs 的ng-view。不然只能哪里用到，哪里调用

---

** JS SDK可以增加模糊查询吗 **  
目前JS并没有该接口，可使用JS的网络访问接口调用restful api实现，restful api中含有模糊查询的功能。

---

** 我需要将数据加密后再保存到Bmob表吗？ **  
所有SDK到服务器之间的数据都是经过对称加密算法加密后传输的。

---

** JavaScript怎么在bomb数据库里面存入date类型。 **  
```
var number = 42;
var string = "the number is " + number;
var date = new Date();
var array = [string, number];
var object = { number: number, string: string };

var bigObject = new BigObject();
bigObject.set("myNumber", number);
bigObject.set("myString", string);
bigObject.set("myDate", date);
bigObject.set("myArray", array);
bigObject.set("myObject", object);
bigObject.set("myNull", null);
bigObject.save();
```


---

** bmob的query查询可以做对指定列做sum之类的聚合查询吗？ **  
可以。具体查看JS使用文档

---

** JS版里有多图片上传吗 **  
JS版没有多图片上传，需要自行处理

---

** js中用户登录返回的session是不是都一样？ **  
同一个用户多次登录返回的SessionToken是一样

### PHP

** php为什么添加数据的时候字段的值为中文就会出错 **  
检查下你的php编码，建议改为utf-8编码。

---

** 有没有ts的sdk **  
php的sdk只有一个

---

** 使用PHP CURL 推送消息的代码，推送不成功,能否给个例子 **  
请检查证书是否设置好

---

** 操作数据库的话，比如更新两个表，数据回滚有没有？ **  
Bmob暂时没有事务操作，你要想同时更新两个表的话，可以使用批量操作。

---

** test.php出现unauthorized
下载sdk之后，修改了配置文件的Application ID和REST API Key
运行test.php出现BmobException: [0]: unauthorized 
app id 或 restful key不正确

---

** php 这边可以插入关联对象吗？ **  
现在官方有生成关联对象的方法 ：
具体在bmob官方php接口中的BmobRestClient.class.php文件中的dataType()方法,可以自行阅读

---

** bmob 最多能取多少条数据 **  
一次最多1000条

---

** bmob bql多表查询如何实现 **  
目前不支持多表查询

---

** php如何使用get（）方法取得不只100条数据？(PHPSDK如何循环获取数据?) **  
请使用分页查询，设置limit值，limit值默认为100，可以根据需要进行设置，具体可查看php文档https://github.com/bmob/bmob-php-sdk/tree/master/doc_develop中的分页查询章节

---

** 获取表中所有数据后怎么单个输出自己需要的数据 **  
查询后返回的是对象数组，您只需要遍历该数组即可。

---

** PC上如何使用Bmob？PC上只能用C#和PHP开发吗？ **  
PHP是我们官方出的SDK，你还可以根据restapi文档开发更多的SDK，非常简单。开发的时候需要注意点的是：1、https协议的问题； 2、header 和 body 的问题； 3、发送方式的问题，如POST、GET、PUT、DELETE。
 

---

** 我有两个表，_User可以放用户的数据，另一个表的password怎么设置成密码？ **  
只有使用_User表的密码才能使用BmobUser的功能，否则接口需要自己再写

---

** 实时数据是什么原理？是客户端轮询吗？ **  
客户端与服务器维护了一个长连接，有消息时由服务端主动推送消息


### Restful

** RestApi 如何进行ACL查询呢？比如有一张表，设置了某条数据，某个用户才能读取查看，那该用户如何获取该条数据呢使用RestApi **  
普通的查询就可以获取了，只要设置了ACL，其它使用就是正常的读写，如果没有权限会有提示

---

** 上传成功，移动文件位置，请问keyoffile 和group代表什么？请问我用C#调用restApi上传文件成功，想把文件移动到指定的位置，文档说用PUT请求，发送data： {keyOfFile:{"__type":"File","group":"upyun","filename": fileName, url: url}，请问里面的keyoffile 和group代表什么 **  
keyOfFile表示你存文件的那个表的字段名，group填个group1就可以了

---

** STM32主板上其他模块获取到的数据怎么通过GPRS上传到服务器上 **  
得看你的板子是否支持https请求，如果支持https请求则可以直接使用restful接口进行上传

---

** RESTAPI 的文档中提到了发送请求创建ACL规则时的body内容，请问发送该请求时的url是什么？ **  
访问哪张表，就给那张表的acl字段进行更新就可以了

---

** bql是否支持limit order by **  
支持，写法如下bql=select * from VersionInfo limit 0,1 order by -version，limit 后面跟两个参数，第一个表示跳过的记录，第二个表示返回的记录数

---

** restAPI只能通过443端口https访问不能通过80http访问吗？ **  
是的，只能通过htts访问

---

** RestApi如何让数据库的某一字段增加1 **  
使用原子计算器来实现

---

** 想通过GPRS模块利用tcp协议上传数据，利用restapi，怎么确认云服务器的ip地址？ **  
restapi都是通过https协议来进行请求的


--- 

** 在Android应用中，不使用BmobSDK，仅用RestAPI, 做到接收推送消息 **  
发布推送可以不使用sdk，但接收推送需要用到。

---

** C++ 使用curl post 数据产生中文乱码 **  
把文件改为 UTF-8 无BOM格式

---

** restAPI 使用短信验证码进行密码重置问题  
用短信验证码进行密码重置 的接口 https://api.bmob.cn/1/resetPasswordBySmsCode ，从接口描述来看，需要上传的信息只有 验证码和新密码，用户的 session 或手机号都不需要上传。  
那后台如何知道这个验证码是哪个手机号发来的呢？ **  
后台是根据你的手机号来生成验证码的，服务端可以知道具体的验证码对应哪个手机号，请放心使用

---

** 我需要多图上传，云端数据库的表应该怎么处理多图逻辑，类似于qq空间的多图上传。 **  
可以在图片上传后把url保存在一个数组当中

---

** 如何用Rest api创建表设置唯一键 **  
唯一键的的设置暂时没有开放restapi接口，我们会考虑进去，后续加入。

---

** 使用Pointer能否“反向”查询？ **  
有一个用户表User，一个公司表Company。每个用户都有一个Pointer字段指向某一个公司。请问如何在查询公司信息的时候，一次性把公司包含的所有用户都查出来？  
目前没有这样的功能，只能在查询到具体的公司信息后，再用Company对象去约束用户表，把该公司下的用户信息查询出来

---

** 可否使用C++集成 **  
用restapi文档对接C++就可以了

---

** 如何比较updatedAt字段 **  
例:where={"createdAt":{"$gte":{"__type":"Date","iso":"2011-08-21 18:02:52"}}}

---

** 想要测试一下平台的短信服务，出现错误10011 no remaining number for send messages. 该账户无可用的发送短信条数，每个账号不是存在100条可用短信吗？ **  
除了100条限制外还有以下限制的，短信发送限制规则是1/分钟，5/小时，10/天。即对于一个应用来说，一天给同一手机号发送短信不能超过10条，一小时给同一手机号发送短信不能超过5条，一分钟给同一手机号发送短信不能超过1条。

---

** 如果列没数据为空，返回行据然列字段名都不返回 **  
Bmob使用的MongoDB数据库，该数据库是无模式的，也就是说您并不需要事先设置列值，而对于某个对象，如果你没有明确设置其值，那么该值就是空的，不存在默认值。

---

** 我在一张表中加关系性字段，为什么是在关联表里新建一行，而不可以选择关联表里已经存在的对象 **  
目前只能通过请求添加relation关系，web端无法添加。

---

** 在【快速入门】【RestAPI快速入门】的CURL例子中的URL的“GameScore”是什么意思？  
在【快速入门】【RestAPI快速入门】的CURL例子中的URL的“GameScore”是什么意思？我需要将这个"GameScore"改为我的应用名字吗？还是改成我的表的名字？ **  
GameScore是表名，你可以改为你自己的表的名字。
application id才是对应你的应用。

---

** restAPI一个post请求后，提示error：unauthorized是什么意思 **  
发送方式有问题，没有把application id 和 rest key正确发送到Bmob后端

---

** 使用httpClient POST请求一个接口返回的错误信息content is empty. **  
错误的含义：post请求里body内容为空

---

** Master Key不能用在RestApi上吗？ **  
可以。masterkey是超级权限，不会受到表是否只读的限制，对于restapi、云端代码和SDK都一样的。

---

** restApi中注册用户邮箱验证功能，可不可以在注册时emailVerified直接赋true **  
不行的，emailVerified是系统内置的字段，后端有邮件的触发行为，不能直接的赋值为true。如果你不想用这个字段，完全忽略就可以了。

---

** restApi查询表可以去掉重复的记录吗 就像sql的 distinct **  
暂无该功能。

---

** restapi 过滤用中文过滤不了。  
where={"name":"guangzhou"} 这个ok  
where={"name":"广州"} 这个不行 **  
注意使用urlencode编码，不会存在中文匹配不了的问题的。

---

** ajax不支持非标准的http请求头，像“X-Bmob-Application-Id”这种非标准的请求头，在ajax中是不被接受的，当ajax请求中设置了“X-Bmob-Application-Id”，这个请求的method就变成了"options"这个非标准的方法。 **  
js的调用请使用bmob提供的js sdk，在sdk中已经解决了这个问题

---

** 在我不知道用户密码的情况下 可以通过其他字段进行查询user用户表吗 **  
可以查询

---

**  如何在线测试RestApi **  
使用Chrome浏览器的Postman插件就可以进行调试了。[点击链接Postman下载地址](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?utm_source=chrome-ntp-icon)。  

界面效果[点击这里查看](http://docs.bmob.cn/restful/faststart/index.html?menukey=fast_start&key=start_restful#RestAPI调试工具)。

---
** Postman发起数据请求没有反应 **  
首先先检查本地网络，通常是因为本地网络或者Postman没有成功发出数据请求，其次可以打开[https://api.bmob.cn/](https://api.bmob.cn/)查看是否能打开进行测试。

---

** 其他语言用RestApi开发遇到请求security的错误 **  
请查找相关语言访问HTTPS的配置问题。
如PHP用CURL开发时，需要添加如下脚本：

```java
curl_setopt($c, CURLOPT_SSL_VERIFYPEER, FALSE);
curl_setopt($c, CURLOPT_SSL_VERIFYHOST, FALSE);
```

---

** 能提供Java调用RestApi的示例代码吗 **  
点击下面的链接可以看到Java调用RestApi的示例代码：

[http://wenda.bmob.cn//?/question/51](http://wenda.bmob.cn//?/question/51)

[http://wenda.bmob.cn/?/question/859](http://wenda.bmob.cn/?/question/859)

---

** 关于where条件的问题 **  
有开发者提出用PostMan请求的时候没有问题，但是用Java请求构造了where查询条件的时候有错（请求的格式大致如， `https://api.bmob.cn/1/classes/Footballer?limit=20&where={"location": {"$nearSphere": {"__type": "GeoPoint","latitude": 32.31735060,"longitude": 118.32457035 }}}` ）。  

这个问题是因为特殊字符导致的问题，大家可以参考以下的解决方案：  

[http://stackoverflow.com/questions/636770/is-there-any-java-equivalent-of-phps-http-build-query-function](http://stackoverflow.com/questions/636770/is-there-any-java-equivalent-of-phps-http-build-query-function)

顺便说一句，PHP中的话，可以直接用`http_build_query`方法构造请求参数。

---

** Restapi有IM吗？ **  
restapi可以发送推送信息，也可以通过get的方式获取聊天内容，但没有开放长连接服务，也就是说用restapi可以实现im功能，但方法只能通过定时器+get数据的方式。

---

** 哪里可以看到错误码 **  
[点击这里](http://doc.bmob.cn/other/error_code/)可以查看错误码列表。


## 云函数常见问题

** 使用云函数需要掌握什么语言 **  
`Javascript`，因为云函数是用`Nodejs`部署架构的。

---
** 云函数能做什么事情 **  
云函数的推出是为了给大家解决更多后端业务逻辑的问题，让大家尽可能把更多的业务逻辑挪到云端，实现更快的更新迭代。目前，云函数除可以自由操作云端数据库外，还提供了`邮件模块`、`HTTP模块`和`事件模块`等，方便大家自由发挥。

---
** 云函数能上传文件吗 **  
暂不支持。

---
** 如何调试云函数 **  
- Bmob在Web端（当前云函数的下边）为大家提供最简单的云函数的调试工具。
- 云函数本地化调试工具：[https://github.com/bmob/bmob-cloud-tool](https://github.com/bmob/bmob-cloud-tool) 。


---
** 云函数或者android上update能否不用objectid用组合条件 **  
只能根据objectid来，在查询返回的结果集中有objectid

---
** 云函数，可以把消息发给IMSDK吗 **  
目前不可以。

---
** url转码怎么转  **  
encodeURI(url)

---
** 如何使用同步的ohttp.post请求 **  
用eventproxy

---
** 相同的代码，在Local中可以返回正确的结果，在Server中返回错误。请问如何解决？ **  
把本地的nodejs版本改成和云端一样，然后调试通过就可以了

---
** bmob的短信服务端验证接口云函数怎么做？要发送一个post请求 **  
使用云函数发送http请求即可

---
** 生成新应用时云函数没有复制到新应用 **  
可使用云函数的本地调试工具可以运行后可以直接导入

---
** 云函数能否实现 WebSocket ？ **  
云函数无法使用第三方库

---
** 往表中添加基本类型的数据是调用数据库对象的insert方法，而添加关联关系对象是用add方法？？那我的表里有这两种数据类型，该怎么添加数据 **  
分别存储

---
** 保存一个Object类型字段的值为null的时候会报错 **  
保存为这样{}

---
** 如何实现一个签到的逻辑 **  
在用户表添加一个字段--签到时间，当用户发送请求的时候，更新这个签到时间，如果签到时间为今天，说明已经签到

---
** where语句如何查询24小时之前创建的记录？ **  
查询createdAt在24小时之前的记录就可以了

---
** 删除数据库记录只能用objectId吗？不能用where条件吗 **  
只能用objectId,where条件用于查询，查询后的结果集中会有ObjectId的。

---
** 云函数怎么设定where条件 **  
```
"where":{
"updatedAt":{
"$lt":{"__type":"Date","iso":"2014-01-29 11:33:53"}
}

```

---
** 在查找数据库的回调里面再查找，不能收到回调消息 **  
```
db.find(
{
"table":strTableName,
"count":1,
"limit":0,
},
function(err1,data1)
{ 
var searchNum = data1; //表的总行数，用sql语句获得
var limitnum=1000; //默认最多返回1000条记录
var runcount= parseInt(searchNum/1000); 
var strOutID = '';

//分多次获取记录，因为每次只能获取1000条
var i = 0;

for(i = 0;i !== runcount; i++){

var skipNum= 1000*i;
if( i==runcount ) {
limitnum=searchNum-skipNum;
} else {
limitnum=1000;
}
//能执行到这里，
//response.send('data1'); 
db.find(
{
"table":strTableName,
"count":1,
"limit":0,
},
function(err2,data2)
{
//这里执行不到
response.send('data2'); 
}
);
} 
}
);
```

不能这样取，只能取一次，然后再取一次，不能在里面for循环

---
** 云函数可以查询支付订单吗？返回订单结果和数额之类的，有相关函数吗 **  
可以使用云函数去调用restful接口来查询

---
** 云函数可以实现抓取别的网页信息吗？比如说，我客户端去请求云函数，让云函数实现抓取某个咨询网站的信息 **  
可以，使用云函数的http请求抓取即可。

---
** 请问云函数可以发送短信吗？ **  
可以通过云函数调用restful接口来实现。

---

** 云函数更新用户表错误，但是最后返回的err包含错误信息  
{"code":206,"message":"User cannot be altered without sessionToken Error."} **  

必须先登录才能更新

---
** 请问云函数怎么返回JSON数据 **  

```
var data = { dir: 'kunhony', param: 'archive' };
var str = JSON.stringify(data);
response.end(str);
```

---

** 如何在云端请求微信 **  

http://doc.bmob.cn/cloud_function/web/

---

** Bmob中如何支持Cookie？用于将SessionID分配给浏览器 **  

不支持set-cookie的方法。

---

** 请问云函数如何返回错误？ **  

如下，代码一般为这种形式，如果错误，返回response.send(err);

```
function onRequest(request, response, modules) {

var functions = modules.oFunctions;

functions.run({
   "name": "test",
   "data":{"content":"你好","address":"guangzhou"}
},function(err,data){
   //回调函数
   if(err){
       response.send(err);
    }else {
       response.send(data);
    }
});
}
```

---

** 开发公众号可以获取微信的openid吗 **  

可以

---

** 云函数如何进行模糊查询 **  

调用restful的模糊查询接口

---

** 云函数能引入第三方模块吗？如underscore **  

不可以，如要使用第三方模块，可考虑使用窗口服务。

---

** 我有一个云函数，客户端访问的时候查看一条数据库对象，如果不存在，则创建、返回，如果存在则直接返回。所有客户端的访问都是查看同一个对象，如何保证多个客户端同时访问的时候不会同时创建多个对象？ **  

目前这个无法做到。

---

** bql不支持 delete语句吗 **

目前bql只支持查询语句。

---

** 表设置了 ACL， 我想用 master key 或 用户的 token 去更新表，在云端用批量更新模块，如何传入master key 或 用户的 token ？ **

目前不支持

---

** 云函数怎么延迟执行一个操作 **

目前并无该项功能

---

** 云函数中不同的模块中经常出现相同代码 有没有办法把这些代码提取到公共区域来复用 **

云函数之间是可以相互调用的，具体查看云函数云对象章节。

---

** 如何清空某个数据表？ **

需要先将表的所有值查询下来，然后遍历去删除，具体参考文档的查询及删除对象章节


---

** 怎么在云端调用 获取短信验证码、验证短信验证码 **

使用云函数进行http请求，请求RESTful接口即可

---

** 云端如何自定义返回数据 **

定义好格式后以JSON形式返回

---

** 云函数MD5加密中文，结果怎么和PHP的不一样？ **

编码问题，https://cnodejs.org/topic/54ad4e40ce87bace2444cc49

---

** BMOB云端数据库导入需手动导入CSV格式，如何做到自动抓取我本地CSV文件传入云端数据库 **

Bmob导入数据，只可以从web后台手动导入。如果你要自动从本地传入数据库的话，可以自己写代码（程序）实现，用Bmob提供的SDK或基于RestApi来插入数据到云端数据库中。

---

** 云端数据库更新需上传CSV文件，如何实现自动云端更新 **

云端数据库与你本地数据库的结构可能会有区别，需要你针对自己的数据库特点，读取本地数据库，转换后再进行上传

---

** 用云端查询db.find，查询到表里的数据，返回的字段名也是表的列名，有没有像sql里面as的方式修改这个名字 **

目前还没有这个功能

---

** 如果一个字段里没有值，查询后返回的内容也没有这个字段，如果才能让这个字段也出现在返回的内容里。 **

由于后台使用的是MongoDB，是无模式的，没有初始值，因此只有显示地给该字段赋值才会有内容返回。

---

** 写云函数的时候，只能通过objectId来查询符合条件的一行数据？我想用表中的其他字段当做查询条件怎么写? **

可以使用条件查询，具体查看数据库对象中的查询多条数据小节。

---

** 用skip和limit来实现分页查询的话，如果表里的数据更新的很快的话，会不会查询出重复的数据？ **

会出现重复数据，因此，一般您在查询时可以加上限制，比如，查询第一页时的时间为A，那您可以约束查询创建时间在A之前的数据，在那之后的数据不查询，这样就不会有重复了。

---

** 该如何实现类似乐观锁的功能 **

目前并没有提供该类型的接口

---

** 连上vpn没有数据返回 **

可以在连上VPN时ping https://api.bmob.cn/看看能否ping通，有可能是VPN屏蔽了

---

** 云函数中where条件怎么表示!=？ **

您好，可以参考restful文档中的查询数据中的条件查询，大概的形式为"type":{"$ne":"delete"}

---

** 如何更新1000条以上的记录 **

可以采用分页，先取1000条数据进行更新，再取1000条之后的数据接着更新

---

** 请问云函数请求HTTP时如何获取cookies和带cookies访问？ **

将var http = modules.oHttp；
改成var http = modules.oHttp.defaults({jar: true});
即可使用全局cookie，后面的链接就不需要手动输入cookie了。

---

** JavaScript能调用云函数吗（xx平台能调用云函数） **

只要支持https请求就可以通过restful来调用云函数，部分sdk直接封装了调用云函数的接口，具体可以查看云函数文档。

---

** 请问云端new Date()如何获取和createTime里面一样的时间 **

createAt这个属性是特殊字段，为了节约HTTP流量，我们没有进行特殊字段类型处理，直接返回string类型。你在云函数里面new Date()获取的是一样的时间，因为服务器的时间是保持一致的。至于两者的数据格式问题，你可以自行处理。

---

** 云函数数据库可以返回多少条记录？ **

一次最多只能返回1000次数据，如果要获取的数据大于整个数目，必须要分多次查询

---

** 云函数只能添加方法吗 **
我想在云函数中添加一个功能模块，但是发现云函数中的每个文件都是独立的，而且只能是方法，我想问一下能不能实现。

完全可以在方法内声明方法或者类的，这个不影响，而且可以通过间接调用的方式调用其他云函数的执行。

---

** webstorm在本地搭好服务器，在不联网的情况下，使用ios调用运行在本地的服务端代码，能不能利用这样的方式测试？ **

不可以，数据保存在云端，不联网无法操作数据，本地调试过程中不需要客户端的参与。

---

** 云函数执行console.log无输出 **

在真正的云函数上，不支持console.log这种输出，只能使用res.end()

---

** 云端怎么实现 var wpwp = require('wpwp')('YOUR-KEY'); **

云函数进行了封装，无法加载非官方模块。

---

** 如何更新数据表中Date的数据 **



```
var userData = dataObject.results[0];
var checkDate = userData.checkDate.iso;

var lastDate = new Date(checkDate.toString());
var nowDate = new Date();

db.setHeader({"x-bmob-session-token":request.body.sessionToken.toString()});
userData.checkDate.iso=nowDate;
db.updateUserByObjectId({"objectId":request.body.objectId.toString() ,data: {"checkDate":userData.checkDate,"diamond":parseInt(userData.diamond)+10}},function(err,data)
{
})
```

---

** containedIn在云函数里面是什么指令 **

对应为 [RESTful开发文档](http://doc.bmob.cn/data/restful/develop_doc/) 查询小节里面的 $in 查询，你可以参考restful文档，在where条件中使用就可以了。

---

** 如何在云函数中计算两个时间的时间差 **



```
var lastDate;//一定要是Date哦
var nowDate = new Date(data); 

Date.parse(nowDate) - Date.parse(lastDate)

//注意：单位是毫秒级的哦
```


---

** 批量操作对象中 "path": "/1/classes/GameScore" ，其中的 "/1/class/ "是什么来的？怎么确定下来的？ **

/1/classse/ 是系统规定的路径，其中1是系统内部的版本号，classes表示接下来要操作的是数据表。

---

** 云函数能不能实现函数递归调用 **

可以，但要注意不能过于复杂，5s内无回调会提示超时。

---

** 我想用云函数修改user表中的数组，要如何设置？如何先获取表中的数组呢？获取了之后又要如何用arr.addUnique更新？求示例。 **

要修改User表中的数据需要注意：
1. 要么你有登录用户的sessionToken信息（也就是权限），这样可以修改用户信息；
2. 要么你用masterKey（也就是超级权限）来修改用户信息。

获取表中的信息非常简单，你直接Get就可以了，获取之后，你直接用类似如下的方法解决：
```
var arr = modules.oArray;
arr.addUnique({
"table":"_User",

"objectId":"j4w2DDDT", //这个对应是这个用户的objectId
"data":{"skills":{"__op":"AddUnique","objects":["flying","kungfu"]}}

},function(err,data){
//回调函数
});
```

---

** 云函数比较复杂的时候，很难找出根本原因 **
1. 能否支持加入日志，通过查看日志来debug？
2. 能否有类似IDE的断点，或者是报错信息更明确一点在哪里出错？

可以借助我们开发的这个云函数本地化调试工具来调试：
https://github.com/bmob/bmob-cloud-tool

---

** 对于设置了ACL为用户只读的数据，如何在云函数里将其全部读出？ **

使用masterKey
云函数设置masterkey的方法：
```
function onRequest(request, response, modules) {
var db = modules.oData;
db.setHeader({"X-Bmob-Master-Key":"这里填写Master Key信息"});
db.updateUserByObjectId({"objectId":"这里是需要更新的用户ObjectId信息" ,data:{"username":"123"}},function(err,data){
response.end("更新成功");
}); 
}
```

---

** 如果把代码放在云端，本地JS调用时，是否需要输入Application ID、REST API Key才能进行调用呢？ **

只需要在初始化js sdk的时候传人Application ID、REST API Key就行了，在js调用云函数的时候不需要传入

---

** 云函数里如何获取当前时间 **

云函数是运行在nodejs的环境中，所以js的函数能用在云函数上。
获取时间： var now = new Date();

---

** 调用云函数，能否获取调用者的真实IP,想用IP来做排行榜的地理位置统计 **

云函数打印headers

```
function onRequest(request, response, modules) {
response.send(request.headers);
} 
```

结果：

```
Response Body
{
"code": 200,
"msg":
{
"x-real-ip": "114.114.114.114",
"x-forwarded-for": "114.114.114.114",
"host": "cloud.bmob.cn",
"x-nginx-proxy": "true",
"connection": "close",
"accept": "/",
"a": "",
"content-length": "7",
"content-type": "application/x-www-form-urlencoded"
}
}
```

x-real-ip就是用户的真实ip的


---

** 请问怎么查询用户当前排名 **
比如:我有个GameScore 表 
字段有:username,score
现在排行榜里面数据有5000多条，我知道某个用户objectId，如果快速找出排名位置呢？

解决方案：
根据order排名，把所有排名按次序放到一个数组中，然后根据objectId查找到某个用户名，用户名在这个数组中的位置即是他的排名。 
RestAPI查询条件如下：
第一步：先查询到某个用户的用户名：

```
curl -X GET \
-H "X-Bmob-Application-Id: Your Application ID" \
-H "X-Bmob-REST-API-Key: Your REST API Key" \
-G \
--data-urlencode 'keys=username' \
https://api.bmob.cn/1/users/某个用户的objectId
```

第二步：score降序获取前1000名的用户的用户名：
```
curl -X GET \
-H "X-Bmob-Application-Id: Your Application ID" \
-H "X-Bmob-REST-API-Key: Your REST API Key" \
-G \
--data-urlencode 'keys=username&order=-score&count=true&limit=1000&skip=0' \
https://api.bmob.cn/1/classes/GameScore
```
返回前1000名的用户名，判断前一个查询的用户名是否在这个数组的哪个位置，如果没有找到，继续第二步, skip设为1000，直到找到为止。

优化方案：
GameScore应该添加Pointer类型指向某个用户，然后在GameScore添加一个排名的列，更新score的时候更新排名，这样就可以直接根据用户的objectId一条查询就出来了。


** 本地iOS工程怎么调用云函数 **  
[云函数iOS开发文档](http://doc.bmob.cn/cloud_function/ios/)


## 短信服务常见问题

** 购买方法及发票问题 **  
登录开发者后台-->点击某个应用-->短信-->短信信息-->充值 里面进行自由购买。
需要发票报销的可以联系客服开具发票。

---
** 为什么有时候收不到短信 **  
请检查你是否短时间内给同一个手机号码发送了多次短信，短信发送限制规则是1/分钟，5/小时，10/天。即对于一个应用来说，一天给同一手机号发送短信不能超过10条，一小时给同一手机号发送短信不能超过5条，一分钟给同一手机号发送短信不能超过1条。  
还有一种情况是回复过TD退订的会被运营商列为黑名单，该通道不回再给该号码发送任何短信信息。如需要接收信息，需要在官网上联系客服QQ解封。

---
** 短信服务的签名可以换成我们自己定义的吗 **  
短信服务支持自定义签名，只需要在控制台短信设置处进行设置即可。
 
---
** 提交短信验证码模板时需注意什么 **  
1.模板中不能有【】和 [] ，否则审核不通过。  
2.如果你提交的短信模板无法发送，则有可能包含一些敏感监控词，具体可去Github下载 [短信关键字监控参考文档](https://github.com/bmob/bmob-public-docs/blob/master/%E7%9F%AD%E4%BF%A1%E5%85%B3%E9%94%AE%E5%AD%97%E7%9B%91%E6%8E%A7%E5%8F%82%E8%80%83%E6%96%87%E6%A1%A3.doc) 来查看提交内容是否合法。  
3.一天一个应用给同一手机号发送的短信不能超过10条，否则会报10010错误，其他错误码可查看 [错误码](http://doc.bmob.cn/other/error_code/) 。

---
** 注册短信验证码发送以后多久后才能重发 **  
短信发送限制规则是1/分钟，5/小时，10/天。即对于一个应用来说，一天给同一手机号发送短信不能超过10条，一小时给同一手机号发送短信不能超过5条，一分钟给同一手机号发送短信不能超过1条

---
** 当使用不是Bmob的短信功能时,如何通过短信找回密码？现在短信验证mob(shard sdk)是免费的,而bmob的收费的.像我们这种没资本的开发者只能刚开始是用免费的,所以注册时都是用mob的短信sdk进行验证.但是假如有一天用户的密码忘记了.想通过短信的方式来找回的话.那么就不能用mob的短信功能来做了.只能通过bmob的邮箱方式,但是作为手机端这个显然是体验不好 **  
可以结合云端代码来解决。用mob验证验证码成功之后，就用 云端代码+master key 的方式，修改_User表的密码记录。


### iOS

** iOS 新安装的短信SDK 和之前安装的BmobSDK有冲突 **  
短信SDK是在不需要使用BmobSDK时才使用的，BmobSDK里本身包含的短信SDK的所有内容，所以你将短信SDK移除就可以了

---

** 手机验证码注册不成功 **  
如果注册前不验证验证码是否正确，直接发送注册请求，就可以注册成功，如果先验证，就会报错。提示：code error 207 ，输入的验证码是正确的。请问如何解决。

```
- (IBAction)registerNewUser:(id)sender {
// 验证注册码是否正确
[BmobSMS verifySMSCodeInBackgroundWithPhoneNumber:self.phoneNumber.text andSMSCode:self.smsNumber.text resultBlock:^(BOOL isSuccessful, NSError *error) {
if (isSuccessful) {
// 发送注册请求
BmobUser *buser = [[BmobUser alloc]init];
[buser setUsername:self.phoneNumber.text];
[buser setPassword:self.password.text];
[buser setMobilePhoneNumber:self.phoneNumber.text];

[buser signUpOrLoginInbackgroundWithSMSCode:self.smsNumber.text block:^(BOOL isSuccessful, NSError *error) {

if (isSuccessful) {
NSLog(@"注册成功");
}else{
NSLog(@"注册失败%@",error);
}
}];

}else{

NSLog(@"输入的验证码不正确");
}

}];

}
```

验证码注册只需要在注册的时候输入即可，不需要先进行一次验证的，verifySMSCodeInBackgroundWithPhoneNumber方法是用于注册以后的验证功能

---

** 注册时需要短信验证， 改怎么实现 **  
注册时让用户填写手机号码，再进行验证即可，有手机注册验证接口


## IM服务常见问题

** IM的开源地址是什么？ **  
Android：[bmob-android-im-sdk](https://github.com/bmob/bmob-android-im-sdk)  
iOS : [bmob-iOS-im-sdk](https://github.com/bmob/bmob-iOS-im-sdk)

---
** 为什么我的手机接收不到信息 **  
请先在Web后台配置包名或者证书。

---
** 消息推送的时候我没开启网络，在推送一段时间后再开启网络，会收到消息吗？ **  
在断网开始的一分钟内发的消息是接收不到的，因为心跳包的默认时间是一分钟，这一分钟内，服务器不认为该链接是断开的，所以消息不会保存成离线消息。

---
** Bmob可以做群聊吗？ **  
可以利用[开发文档](http://doc.bmob.cn/data/android/)数据实时同步功能来实现群聊。  

思路可以这样：  
1.创建一个群聊表，包括 群组id信息 发送人信息 聊天信息，这里可以把所有的聊天内容放进去;  
2.创建一个群组信息表，包括 群组用户列表 创建时间 群组名称等;  
3.创建一个群组信息变更表，包括 群组id信息，用一个字段记录有消息新增;

当有人在群组中发起聊天时，首先先往群聊表中新增一条记录，然后往群组信息表更表中更新一下记录。所有群组的人都监听自己群组对应的群组信息表更表的几行。 

---

** 为什么发送位置的时候定位不了 **  
1.如果你是直接用demo里面的bin目录下的apk的话，是不存在这个问题的。  
2.如果你是下载demo之后直接运行的话，需要去重新去百度地图官网申请key,因为demo里面的可以是和我的eclipse绑定在一起的，相信做过百度地图开发的知道这是为什么。

** 我想实现私信功能 应该用IM来实现吗 **  
有两种方案：  
1.使用IM实现  
2.如果私信功能对实时信要求并不是很高，那么也可以将聊天记录放在表中，并且采用定时拉取的方法。

--- 
** im sdk支持群聊活着广播消息么？ **  
SDK内部暂时还没有实现群聊部分，只是在内部预留了相关的接口，方便后续开发而已。


---

** android新版IM不支持好友管理? **  
新版IM不同于旧版IM，不再提供与用户相关的操作了，比如登录、注册、好友管理相关的。开发者可以自行实现

---

** 用自己的key运行新版BmobIMDemo，IM通讯的各种消息的数据库表在哪？（IM即使通讯的注册数据是保存在哪里，BmobIM里面的聊天数据储存在哪个数据库） **  
目前新版IM是没有将发送的消息存储到Bmob后台的，开发者可自行选择存储，sdk的聊天消息都是本地存储的

---
** 不论对方是否为我的好友，开启聊天的方式都是BmobIM.getInstance().startPrivateConversation（）吗？  
意思是说好友和陌生人开启聊天的方式都是一样的?只是好友在聊天列表里方便查找？  
那陌生人的好友的区别在哪里？ 可以在聊天界面的标题 设置类似qq的添加好友吗？ **  

只有会话的概念，没有好友的概念，新版的IM好友管理需要开发者自行实现。

---
** Unity使用Android和iOS的IM的SDK，可以实现即时通讯么？ **  
Unity支持调用android和iOS和IMSDK，可以实现

---

** Bmob Im 是采用什么协议? **  
基于TCP的自定义协议。

---

** 新版本IM兼容老版本吗？ **  
不兼容，新版IM采用全新的协议实现。

---
** 利用数据同步功能实现群聊 **  
答：用数据实时同步实现群聊的思路可以这样：

1.创建一个群聊表，包括 群组id信息 发送人信息 聊天信息，这里可以把所有的聊天内容放进去  
2.创建一个群组信息表，包括 群组用户列表 创建时间 群组名称等  
3.创建一个群组信息变更表，包括 群组id信息，用一个字段记录有消息新增

当有人在群组中发起聊天时，首先先往群聊表中新增一条记录，然后往群组信息表更表中更新一下记录。所有群组的人都监听自己群组对应的群组信息表更表的几行。

热心的用户实现了一个[Android基于Bmob群聊功能的实现](http://blog.csdn.net/shangmingchao/article/details/50548898)


---

** 怎样用邮箱查找用户？ **  

参考查找用户那部分的代码：（如果希望邮箱是唯一的话，还需要在Web后台指定email字段是唯一键）

查询用户
查询用户和查询普通对象一样，只需指定BmobUser类即可，如下：

```
BmobQuery<BmobUser> query = new BmobQuery<BmobUser>();
query.addWhereEqualTo("email", "heshaoyue@bmob.cn");
query.findObjects(this, new FindListener<BmobUser>() {
@Override
public void onSuccess(List<BmobUser> object) {
// TODO Auto-generated method stub
//这里得到的就是用户信息
toast("查询用户邮箱成功："+object.size());
}
@Override
public void onError(int code, String msg) {
// TODO Auto-generated method stub
toast("查询用户失败："+msg);
}
});
```

---

** 为什么我们离线能接受到消息呢？我们登陆的时候是不是因为服务器知道我们的帐号id再某个地方登陆了，就把消息推送到那个设备上，那么我们离线的时候下次再上线能接受到消息是怎么做到的？ **  
离线消息这个需要服务端支撑的，服务端在向特定用户（设备）下发消息的时候，会去检测下当前用户的客户端连接是否正常，如果连接已经关闭了，表明该设备下线或者处于关机状态，此时服务端会将发给该用户的所有消息凑存在一个数组中，之后在等该用户上线（重新建立连接）的时候，服务器会再将这些离线消息按照时间先后顺序依次下发给该用户。

---

** 使用了IM组件，推送怎么搞？ **  
最新版本的IM不需要再使用推送，如果需要在用户离线时使用推送功能，可以直接使用推送sdk推送内容。

---

** 为什么IM组件在有的手机上可以接受到聊天推送，有的手机上就接收不到呢？ **  
有一些定制过的机器，比如小米、魅族这些，你根据系统的情况做一下处理。

---

** 一个用户发送消息，另一个用户怎么知道他发送消息了。里面的工作原理是什么 **  
首先，两个用户对应的终端都跟Bmob服务器保持了一个心跳长连接服务，这样的话，终端和服务器端就可以双通道通讯了。

接着，一个用户发送消息给另外一个用户，消息首先到Bmob服务器，Bmob服务器根据消息的内容体判断是发给哪个终端，然后再把消息发送下去。

整个的工作原理就是：websocket长连接。

---

** 关于 BmobRealTimeData 的几个问题 **  
1.isConnected() 的返回结果是实时更新的吗？比如用户本来连接成功，但是过一会儿没有网络了，再调用该函数是不是会返回false？  
2.失去网络连接，然后又恢复网络连接后，BmobRealTimeData 实例会不会自动重连？  
3.这个是基于长连接的吗？耗电情况如何？

答:
1.实时的,没有网络返回false.  
2.会自动重连  
3.长连接, websocket,不会怎么耗电,你可以自行测试下

---

** 在IMSDK中如何获得用户的状态（在线，或下线，无打扰，等） **  
可以定时（比如5分钟）更新一下用户表，这样就可以通过用户表的updatedAt和当前时间的比较，知道用户是否在线了。

---

** BmobI'M2.0 有没有系统消息功能 **  
没有，需要用户自行扩展

---

** 发送请求添加好友，BmobIMUserInfo 是发送方，还是接收方的信息啊？ **  
发送方的信息，SDK内部已经弄好了，给别人发送消息，肯定需要接收方的信息

---

** 新版本IM是不是没有附近的人这个功能了 **  
新版IM已经不提供这样的功能了，这些功能开发者可以自行封装，新版IM采用的是全新架构，只负责消息的发送和接收，并不再提供与具体业务逻辑相关的API方法


### Android

** 我看了官网即时聊天的demo，同样都是继承BombObject的javabean类（数据表）为什么有的是创建在云端，有的保存在本地数据库？这是怎么设置的 **

自己控制的呀，想保存到后台，那你就调用save方法来创建数据，保存到本地就自己创建数据库

---
** BmobIM2.0 发送自定义消息失败 **

```
SendCommentMessage commentMessage=new SendCommentMessage();
            User currentUser = BmobUser.getCurrentUser(DynamicDetailActivity.this,User.class);
            Map<String,Object> map =new HashMap<>();
            map.put("name", currentUser.getUsername());//发送者姓名，这里只是举个例子，其实可以不需要传发送者的信息过去
            map.put("avatar",currentUser.getAvatar());//发送者的头像
            map.put("dynamicId",dynamicid);//发送者的uid
            //启动一个会话，如果isTransient设置为true,则不会创建在本地会话表中创建记录，
            //设置isTransient设置为false,则会在本地数据库的会话列表中先创建（如果没有）与该用户的会话信息，且将用户信息存储到本地的用户表中
            //构造聊天方的用户信息:传入用户id、用户名和用户头像三个参数
            BmobIMUserInfo info;
            if (atUser!=null){
                info = new BmobIMUserInfo(atUser.getObjectId(),atUser.getUsername(),atUser.getAvatar());
            }else{
                info = new BmobIMUserInfo(dynamic.getAuthor().getObjectId(),dynamic.getAuthor().getUsername(),dynamic.getAuthor().getAvatar());
            }
            BmobIMConversation c = BmobIM.getInstance().startPrivateConversation(info, true,null);
            c.sendMessage(commentMessage, new MessageSendListener() {
                @Override
                public void done(BmobIMMessage bmobIMMessage, BmobException e) {
                    if (bmobIMMessage!=null){

                    }
                }
            });
```

还少了一个步骤，使用obtain方法创建一个用于控制发送消息的会话实例

---

** BmobIMUserInfo info为null  
BmobIMUserInfo info = BmobIM.getInstance().getUserInfo((String) BmobUser.getObjectByKey(mContext, "objectId"));  
info为null是为什么 **

用户信息需要开发者自己调用sdk提供的更新本地用户信息的方法（BmobIM.getInstance().updateUserInfo(BmobIMUserInfo info)）来存储的，然后才能通过getUserInfo方法获取的，因为IMSDK内部维护了一个用户表。

---

** 怎么查询别人要请求添加我为好友的信息？就是想加我好友的人的列表。android，即时通讯，我用另外一个小号发送了请求加我大号为好友的请求，但是我怎么查询出谁发送了这个请求，查询出来后我才能点击同意啊。文档上只说加好友和同意加好友，没说怎么查询列举出添加好友的请求的信息。 **

目前的demo里面的好友添加请求是查询本地数据库的（可查看  
NewFriendActivity中的query方法，NewFriendManager.getInstance(this).getAllNewFriend()方法查询好友添加请求），查询出来的就是谁添加我为好友的请求

---

** Android Im拖动未阅读的会话数量控件调用conversation.updateLocalCache()不能将会话标记为已经阅读 **

conversation.updateLocalCache();这个方法需要先开启私聊并创建会话后拿到的新会话实例才可以调用的，具体可参考ChatActivity中的用法。

---

** Android使用Bmob IM聊天时有离线消息就会闪退 **

android.content.res.Resources$NotFoundException: String resource ID #0x7f060015
你这个错误是因为没有导入bmob_im_notification_strings.xml这个文件造成的。

请查看官方IM文档中关于下载NewIMSDK及官方Demo的描述：
values(bmob_im_notification_strings.xml)-用于通知栏显示

--- 

** 想用聊天组件，连接服务器出错误 **

看Android开发文档中SDK导入部分的解释：

每个版本的im依赖特定版本的bmob-sdk：

bmob-im:1.1.8--->bmob-sdk:3.3.5  
bmob-im:1.1.9--->bmob-sdk:3.4.3  
bmob-im:2.0.1--->bmob-sdk:3.4.6-0304  
bmob-im:2.0.2--->bmob-sdk:3.4.6-0304  
bmob-im:2.0.3--->bmob-sdk:3.4.6  

---

** 发送消息的时候添加的额外参数在接收的时候怎么拿到 **

getExtra返回的是一个字符串，再自行解析。

---

** 用android studio打开后，报不是gradle工程，是啥原因？ **

使用as 是需要依赖gradle来下载各种jar包的，因为需要翻墙下载

### iOS

** BmobIm服务器的消息怎么删除，每次删除程序再打开都会有离线消息 **

这些是服务端自动存储的，并不是保存在表中，而是后端以另一种形式保存，无需用户自行维护～


## 推送服务常见问题

** 推送服务采用的协议是什么 **

`Websocket`

---

** 会不会限制推送消息的数量 **

没有限制！  
推送的用户数量没有限制，每天推送的消息条数也没有限制，所有都没有限制。

---

** 服务器能支撑的长连接有多大 **

Bmob的推送服务器是耗内存型的，保持1个长连接占用<10KB的内存，64GB的内存能够支撑600万用户的长连接。

---

** Android推送收不到消息 **

1.手机是否连入网络  
2.包名（应用包名，看配置文件）是否正确填写在web后台中  
 
如果还是不能接收到推送，请检查：  

3.手机是否有bmob的推送后台在运行  
4.后台的Installation表有没有该手机对应的设备信息

---

** iOS推送接收不到消息 **

iOS的推送都是用apns。你确认是否操作了几点：  
1.检查推送的代码是否写错;   
2.真机操作；  
3.Bmob后台上传了未加密的p12证书；   
4.Bmob数据后台的Installation表是否可以看到对应数据。  
5.push token是否保存到服务器了

---

** 推送的耗电和耗流量情况怎样 **

以下说到的，不考虑推送的内容部分。推送内容的多少是由开发者决定的。

另外，实测电量、流量消耗，与网络状况相关比较大。

所以这里的数据是理论平均值：流量消耗 50K/天，电量消耗 60mAh/天。

---

** 可以推送富文本到客户端吗 **

不直接支持文件的推送，但可以通过推送 url 来实现。
即先推送文件下载 url，到客户端触发逻辑来通过 url 下载文件。

---

** iOS在服务端如何推送有声音和Badge提示 **

需要开发者自己定义JSON格式，格式如下：

```java
{
	"alert" : "You got your emails.",
	"badge" : 9,
	"sound" : "bingbong.aiff"
}
```

### Android

** 手机中安装两个包含bmob push sdk的app，那么这时另一个包含bmobpush sdk的app会报错。 **

解决方法：
删除androidMainfest.xml中
```<permission android:protectionLevel="normal" android:name="cn.bmob.permission.push"></permission>```
这一句。

其实这一句完全可以不加，也可以正常使用，亲测2个app推送正常，且不报错，关于原因请百度android permission相关知识（如果找不到再找客服吧~）

---

** 消息推送后点击消息进入不同的fragment页面 **

这个是需要自己去定义的，在点击进入时应该有一个地方可以控制页面的行为的，具体的谷歌百度会有很多资料

---

** 用PushManager.pushMessage(text)推送的消息能设置过期时间吗？默认的过期时间是多久？ **

暂时没有该功能。

---

** 消息推送里要设置的包名是指什么包 **

消息推送里要设置的包名是你应用的包名（Androidmanifest文件中的package）

### iOS

** 按照设制好了IOS推送，推送后显示状态为“发送至APNS”，但前面写着“推送0条”，此时，手机也未接收到信息，是为什么？ **

1.看看Installation表是否有设备信息；  
2.Bmob后台中是否把推送证书添加上去（不能加密）；  
3.你先尝试推送给所有的真实手机。

---

** 如何用 BmobPush发送原始apns报文？ **

要发送原始信息的可以使用-(void)setData:(NSDictionary *)data;方法

---

** 在iOS中 在代码中如何创建一个空表 只包含各列的属性 而不创建具体的一条数据。 **

参考代码

```
BmobInstallation *ins = [BmobInstallation currentInstallation];
[ins saveInBackgroundWithResultBlock:^(BOOL isSuccessful, NSError *error) {
    if (error) {
        NSLog(@"%@",error);
    } else {
        NSLog(@"success");
        NSLog(@"%@",ins.objectId);
    }
}];
```

---

** 消息推送的条件查询（根据特定的查询条件进行推送）能在自己创建的表格中进行查询条件推送 **

只能使用自带的installation表来查询。

---

** 在installation 表中创立新的列无法添加进去数据 **
```
BmobInstallation *currentIntallation = [BmobInstallation currentInstallation];
[currentIntallation setObject:@"123" forKey:@"classes"];

[currentIntallation saveInBackground];
```
确实是无法直接这么加的，建议使用channel来实现业务需求

---

** 消息推送的条件查询（根据特定的查询条件进行推送）能在自己创建的表格中进行查询条件推送吗？ **

不可以，只能使用自带的installation表来查询


## 支付服务常见问题

** 请问你们的支付sdk怎么收费 **

渠道费和公司税共收取10%。其中渠道费是支付宝/微信收取的费用。

---

** 为什么我支付了0.01但后台看到只有0.00 **

请勿担心，在Bmob财务管理平台订单管理处，金额从小数点后第三位开始不显示，比如支付了0.01元实收0.00，其实是0.0095。

---

** 有哪些其它需要注意的事项 **

支付问题：[点击查看其它注意事项](http://doc.bmob.cn/pay/android/)


** 网页支付的地址到底是什么？(php支付接口报异常) **

因为支付宝安全团队封杀的问题，网页支付暂时不支持，待寻求到解决方案再开放。

---

** 支付 弹出"抱歉，该商户未开通支付宝服务，无法付款" **

如果出现这种情况则表示支付宝账号并封了，bmob需要一定的时间去申请账号重新恢复。

---

** 新版的Android的Bmob Pay一直提示插件已过期 **

运行BP.pay()后会弹出toast显示“bmob pay plugin is out-of-date, please update it”
已经换成5月31日最新版本的sdk了，还是不行

versionCode必须为6和6以上的才是最新版，你可以通过高BP.getPluginVersion来获取

---

** 新版支付SDK里的demo换成我自己的appID为什么不能支付，用Demo里的appID就可以？ **

请创建自己的应用，用自己的appId使用支付SDK。具体的使用方法可以参考Demo和文档。

---

** 微信支付总是返回错误码10003， 是什么原因? 支付宝可以正常使用 **

商品名或者商品描述不符合规范，或者是金额不是double

---

** 移动支付功能是否支持类似美团这种，用户购买了优惠券，资金暂存在我的账户，然后到期后，再由我把钱打给商家 **

购买优惠券存到您的账户可以用我们的支付来实现，您的钱打给商家需要自行实现

---

** Android客户端支付后如何反馈到自己的服务器 **

在web端的“支付”-->”支付配置“里可以填上你自己服务器的url地址，支付成功时会往这个地址发送一些订单成功的数据。

---

** 新版Android支付SDK在虚拟机下测试报错 **

虚拟机上有很多的问题，不支持虚拟机调试。


---

** 微信支付插件在哪里？ **

下载Bmob Android SDK之后，解压，可以看到 assets 文件夹下有一个 BmobPayPlugin.apk ，就是插件

---

** 支付宝支付显示的订单信息，怎么过滤了空格..? name of item ， 显示成了 nameofitem， 是支付宝过滤的空格还是bmob过滤的？这样英文显示不了 **

是我们过滤的，文档中有描述的哦“商品名及商品描述只支持输入中文、英语、数字、下划线(_)及英文破折号(-)，其余字符自动过滤”，这个是由于支付宝那边是这么要求的，如果有除了刚刚说的那些字符外的其它字符会报错，因此我们这边主动过滤了。


---

** 开启验证后数据服务正常但发起支付提示verify error: sign incorrect. **

你在后台开启了应用安全验证并填写了签名，可以在调试时先关掉。发布正式版本时开启

---

** bmob plugin isn't installed 支付这个是什么问题 **

支付功能需要先安装支付插件才能使用

---

** 为什么一直提示支付中断，必须使用支付宝先发起一次支付请求后，然后切换为微信支付，点击支付后才可提示获取订单成功，并跳转至微信支付页面 **

这个问题是因为部分手机（小米手机）不允许未打开过Activity的App访问网络的权限，而支付宝需要先打开Activity，所以可以成功，但微信支付首先是在Service中调用，所以网络请求被拒绝。解决的办法是在BP.pay方法调用之前加上如下代码：
```java
try {
	Intent intent = new Intent(Intent.ACTION_MAIN);
	intent.addCategory(Intent.CATEGORY_LAUNCHER);
	ComponentName cn = new ComponentName("com.bmob.app.sport",
			"com.bmob.app.sport.wxapi.BmobActivity");
	intent.setComponent(cn);
	this.startActivity(intent);
} catch (Throwable e) {
	e.printStackTrace();
}
这段代码加在BP.pay方法调用之前
```
---

** unity怎么使用Bmob的支付呢？ **

参考[这里](http://blog.csdn.net/qq_33747722/article/details/53408000)

---

