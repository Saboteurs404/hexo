MySQL 是最流行的关系型数据库管理系统，在 WEB 应用方面 MySQL 是最好的 RDBMS(Relational Database Management System：关系数据库管理系统)应用软件之一。

在本教程中，会让大家快速掌握 MySQL 的基本知识，并轻松使用 MySQL 数据库。

我使用的 MySQL 版本是 mysql5.6.16，目前 MySQL 最新版为 8.0.22 这里提供官网的下载地址 [MySQL 下载地址](https://dev.mysql.com/downloads/installer/)
我的 MySQL5.6.16 版本的压缩包和安装教程也会提供给大家
下面我将以 MySQL5.6.16 为例，说明 MySQL5.6.16 的安装步骤即存在的问题
首先

**_1. 解压 mysql5.6.16win64.zip 文件到任意文件夹，路径不要有中文，尽量不要放到 C 盘；_**因为有些电脑路径中有问题可能会导致安装成功后 MySQL 无法正常启动

**_2. 打开解压后目录，将 my-default.ini 重命名为 my.ini；_**
***3. 记事本打开压缩包中的 my.ini 文件，将*以下代码进行修改和插入\***
将红括号中的 mysqld 改成 mysql
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104233649473.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70#pic_center)
**_然后在红括号后插入_**

```python
  # 设置mysql客户端默认字符集
      default-character-set=utf8
      [mysqld]
explicit_defaults_for_timestamp=true
    #设置3306端口
      port = 3306
    # 设置mysql的安装目录
      basedir=D:\mysql\mysql-5.6.17-winx64
    # 设置mysql数据库的数据的存放目录
      datadir=D:\mysql\mysql-5.6.17-winx64\data
    # 允许最大连接数
      max_connections=200
    # 服务端使用的字符集默认为8比特编码的latin1字符集
      character-set-server=utf8
    # 创建新表时将使用的默认存储引擎
      default-storage-engine=INNODB

```

**_4.将插入的代码中的 D:\mysql\mysql-5.6.17-winx64 均改为自己解压缩的文件路径，第二个蓝色方框中的 \data 不要删除_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021010423441530.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70#pic_center)
**_5.以上操作全部完成后 ，在开始菜单，找到 windows 系统中的命令提示符 右击以管理员身份运行_**
**_6. 输入加压后文件所在的盘+冒号，（比如‘d:’）回车_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104235309463.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70#pic_center)

**_7. 输入 cd 空格+ 文件路径到 bin 目录 并回车_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104235522755.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70#pic_center)

**_8. 输入：mysqld install 进行安装_**
由于我已经安装过了，所以会显示是这样的
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104235614265.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
前面这部分只要按照操作进行就不会有太大的问题
**_9.接下来需要进行环境变量的配置，右击此电脑选择属性在属性中找到高级系统设置并打开，打开环境变量，_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105000933123.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105001032162.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105001105788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
**_在弹出的界面中，我们选择系统变量下的 Path 双击（Path 本身就存在不用新建）_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105001259193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
**_接下来我们点击新建并浏览本地文件_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105001345247.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105001500202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
**_在本地找到我们所减压的 MySQL 的文件夹下的 bin 目录，点击确定即可_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021010500203885.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
**_接下来我们要进行 mysql 的启动，右击任务栏空白处或者按 CTRL+Ant+del 进入任务管理器，找到 mysql 右击启动即可，_**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105215951459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RlbnNpdHlfXw==,size_16,color_FFFFFF,t_70)
**_如果启动失败，提示框显示未找到说明该文件以被删除或者存放地址已经改变，如果已被删除则需要重新下载需要重新安装，_**
**_如果显示 1067 错误，应该是你的 my.ini 配置有问题，按照上面的教程操作一下，如果你的路径中存在中文也可能导致无法启动，如果你选择更改路径或者重新安装，则需要先将之前的服务进行移除，_**
**_首先你需要以管理员身份打开命令提示符，然后输入 sc delete mysql 或则输入 mysqld --remove 命令即可，至于 mysql 的重新安装，也和之前的输入一样 mysqld install。
至此有关 MySQL 在安装即启动过程中所碰到的问题就都讲完了。_**
