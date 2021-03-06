

## 效果预览
![image](uploads/home.png)
<br/>
后台效果图  <br/>
![image](uploads/admin.png)
<br/>
后台地址：/admin 或者 /login <br/>

## 使用注意
#### 1.开发工具的选择
请使用 IntelliJ IDEA, 尽量不要用 Eclipse/MyEclipse，使用前者项目起不来我可以帮忙解决，后者直接忽视(理论上可以起)

#### 2.确保你安装了 Maven
没有用过 `Maven` 的童鞋，感觉去学一下，安装一下，可以使用 3.3.9 或 3.5.0的版本

#### 3.请安装 Lombok 插件
代码中多次使用 `@Data` 注解，请确保你的 IDE 安装了 `Lombok` 插件，否则找不到 getter/setter 方法

#### 4.确保数据库版本是5.x 版本，8.x版本需要修改配置
对于MySQL8.x版本需要修改 pom.xml 里MySQL驱动版本和数据库驱动名称


#### 5.项目首页没有文件夹名称
确保 tomcat 配置中 `application context` 是 /，而不是 /ForestBlog。这是导致你们首页css样式全无的原因，因为引用css路径都是 /xxx/xxx.css
![image](https://github.com/saysky/ForestBlog/blob/master/uploads/tomcat.png)

具体情况请看步骤

## 使用步骤
任何问题都可以联系我 <br/>
Q Q：847064370 <br/>
微信：847064370 <br/>
在线留言：[https://liuyanzhao.com/message.html](https://liuyanzhao.com/message.html)

#### 1、克隆项目  <br/>
克隆或者下载项目到本地，解压，主要分为三个部分：ForestBlog、uploads 和 forest_blog.sql <br/>
ForestBlog: 完整项目源码, 可以使用 IDEA 导入或者打开  <br/>
uploads: 上传图片的目录，与源码分离开来，可以放到物理磁盘某一目录，如D盘某目录，后面会讲 <br/>
forest_blog.sql: 数据库文件，请先创建数据库，然后以运行sql文件方式导入 <br/>

#### 2.使用 IDEA 导入项目
确保你安装了 Maven，导入项目时，选择已存在的项目，类型是 Maven 项目

#### 3、 导入数据库   <br/>
新建数据库 `forest_blog`，导入数据库（即forest_blog.sql）。注意，数据库的编码和排序规则是utf-8和utf-8_general_ci  <br/>
数据库默认用户名 root，密码 123456

#### 4、修改项目中的数据库连接信息   <br/>
修改 `db.properties` 文件，该文件很容易找到，在 src/main/resources 中<br/>
里面有 MySQL, 请确保已安装和启动 MySQL <br/>
注意修改数据库地址、表名、用户名和密码。<br/>

 
#### 5、配置 uploads 目录   <br/>
该项目中，文件上传是传到本地，且和项目文件夹不在一起，就是说是源码和上传目录是分离的。 <br/>
比如我们把 uploads 目录放到 E盘根目录，比如有一张图片路径是 `E:/uploads/2017/10/avatar.jpg`, 我们想在项目中以 `http://loclahost:8080/uploads/2017/10/avatar.jpg ` 方式访问，需要以下两步：<br/>

1. 修改 UploadFileController.java 中上传路径，需要修改 rootPath 为你指定的 uploads 目录，如 `String rootPath ="E:/uploads/";` <br/>
如果不修改，会出现无法上传失败；<br/>

2. 给 IDEA 设置静态资源映射，在 tomcat 配置中 Deployment 里面添加，如图
![image](https://github.com/saysky/ForestBlog/blob/master/uploads/tomcat2.png)

如果你是在 Linux 服务器上部署，需要在 Tomcat 配置文件中添加 <br/>
在 tomcat/conf/server.xml 的 Host 标签内添加如下代码 <br/>
`<Context path="/uploads" docBase="/www/uploads" debug="0" reloadable="true" />`



