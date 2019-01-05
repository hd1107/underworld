 * [说明](#说明)
      * [术语介绍](#术语介绍)
      * [系统架构](#系统架构)
   * [环境准备](#环境准备)
      * [主机资源](#主机资源)
      * [快速开始](#快速开始)
         * [1. 安装JDK](#1-安装jdk)
         * [2. 安装FTP](#2-安装ftp)
         * [3. 导入数据库脚本](#4-导入数据库脚本)
            * [3.1 metro](#41-metro)
            * [3.2 metrotask](#42-metrotask)
      * [概述及安装包](#概述及安装包)
      * [部署管理节点](#部署管理节点)
      * [部署调用节点](#部署调用节点)
         * [部署64位调用节点](#部署64位调用节点)
         * [部署32为调用节点](#部署32为调用节点)
      * [部署文件下载节点](#部署文件下载节点)
   * [常见问题](#常见问题)
   * [首次初始化](#首次初始化)
   * [版本升级更新](#版本升级更新)


# 说明
本手册适用于铁科院xx平台（以下简称 xx 或『平台』） 0.x系列版本的安装说明，当前的最新版本为 0.xx-GA。
## 术语介绍

* 调用节点 
* 管理节点
* 文件下载节点

## 系统架构
架构图如下:
![架构图](/home/hd/Downloads/underworld/img/tky.png)


# 环境准备
 
## 主机资源
 下表是平台部署需要的详细配置:

 |节点|最小配置|推荐配置|存储|系统版本|
 |---|----|-----|-----|----|
 |管理|4C/8G|4C/16G|200G|Windows Server 2012 R2 (x64) |
 |调用(64)|4C/8G|4C/16G|200G|Windows Server 2012 R2 (x64) |
 |调用(32)|4C/8G|4C/16G|200G|Windows Server 2012 R2 (x64) |
 |文件|4C/8G|4C/16G|200G|Windows Server 2012 R2 (x64) |
 |原始FTP|4C/8G|4C/16G|200G|Windows Server 2012 R2 (x64) |
 |共享FTP|4C/8G|4C/16G|200G|Windows Server 2012 R2 (x64)|
 |SFTP|4C/8G|4C/16G|200G|Windows Server 2012 R2 (x64|

## 快速开始
在节点资源准备好后，开始安装平台需要的公共组件,分为以下几个步骤:
* 安装JDK;
* 安装FTP;
* 配置原始FTP;
* 配置共享FTP;
* 配置SFTP;
* 导入数据库脚本;

需要的软件信息如下表所示:

 |组件名称|版本|大小|备注|
 |---|----|-----|-----|
 |jdk|8u191|207MB|64位|
 |jdk|8u191|197MB|32位|
 |Serve-U|15|19.2MB|
 |tomcat|7.092|10.5MB|


同时在安装的过程中还需要使用的工具如下表所示:

|工具名称|版本|用途|备注|
 |---|----|-----|-----|
 |WinSCP|5.1.3|管理sftp文件|
 |FileZilla|3.38|管理ftp文件|
 |Pl/SQL|11以上|管理数据库|
 |Chrome|54以上|网页浏览器|
 |Postman|6.4|测试api接口|
 |Winrar|5.0|解压缩安装包|
 |Notepad++|7.6.1|修改配置文件|





### 1. 安装JDK
*每个节点必须安装*
1. 双击jdk-8u191-windows-x64.exe运行程序.
![0](/home/hd/Downloads/underworld/img/0.png)

2. 欢迎使用Java SE开发工具包8 Update 191的安装向导界面，点击“下一步”.
![1](/home/hd/Downloads/underworld/img/1.png)

3. 选择安装可选功能界面，默认安装，安装到      C:\Program Files\Java\jdk1.8.0_191。点击“下一步”.
![2](/home/hd/Downloads/underworld/img/2.png)

4. 已成功安装界面，点击关闭
![3](/home/hd/Downloads/underworld/img/3.png)

5. 系统属性界面，在“这台电脑”，右键，属性，高级，环境变量.
 ![5](/home/hd/Downloads/underworld/img/5.png)
 ![6](/home/hd/Downloads/underworld/img/6.png)

6. 新建JAVA_HOME指明JDK安装路径，就是刚才安装时所选择的路径C:\ProgramFiles\Java\Jdk1.8.0_191，此路径下包括lib，bin，jre等文件夹.
 ![7](/home/hd/Downloads/underworld/img/7.png)

7. 寻找 Path 变量在变量值最前输入 ;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin.
 ![8](/home/hd/Downloads/underworld/img/8.png)

8. 新建CLASSPATH 变量,输入: .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar.
 ![4](/home/hd/Downloads/underworld/img/4.png)

9. 检验是否配置成功 运行cmd 输入 java -version （java 和 -version 之间有空格）

若如图所示 显示版本信息 则说明安装和配置成功.
 ![9](/home/hd/Downloads/underworld/img/9.png)






### 2. 安装FTP
平台需要两个FTP节点和一个SFTP节点，三个节点都使用server-u提供服务,安装的过程相同，请按照以下步骤:
#### 安装server-u
1. 双击server-u安装包, 开始安装
 ![1](/home/hd/Downloads/underworld/img/f1.png)

2. 选择接受协议,点击下一步
 ![2](/home/hd/Downloads/underworld/img/f2.png)

3. 选择默认安装目录,点击下一步
 ![3](/home/hd/Downloads/underworld/img/f3.png)

4.  点击下一步
 ![4](/home/hd/Downloads/underworld/img/f4.png)

5. 点击下一步
 ![5](/home/hd/Downloads/underworld/img/f5.png)

6. 点击安装
 ![6](/home/hd/Downloads/underworld/img/f6.png)

7. 开始过程，时长约半分钟
 ![7](/home/hd/Downloads/underworld/img/f7.png)

8. 添加server-u到防火墙例外
 ![8](/home/hd/Downloads/underworld/img/f8.png)

9. 点击完成，server-u安装完成

安装后server-u后开始配置，首先配置共享ftp节点

#### 配置共享FTP
1. 点击桌面任务栏右下角server-u图标,打开控制台.
 ![1](/home/hd/Downloads/underworld/img/c1.png)

2. 点击导航加号按钮，开始配置.
 ![2](/home/hd/Downloads/underworld/img/c2.png)

3. 创建一个新的域，输入域名share,点击下一步.
 ![3](/home/hd/Downloads/underworld/img/c3.png)

4. 点击下一步.
 ![4](/home/hd/Downloads/underworld/img/c4.png)

5. 输入本机的ip地址,192.168.81.121.
 ![5](/home/hd/Downloads/underworld/img/c5.png)

6. 输入需要共享的文件夹 c:/share,点击下一步.
 ![6](/home/hd/Downloads/underworld/img/c6.png)

7. 只选择FTP共享,点击下一步.
 ![7](/home/hd/Downloads/underworld/img/c7.png)

8. 点击下一步.
 ![8](/home/hd/Downloads/underworld/img/c8.png)

9. 点击下一步.
 ![9](/home/hd/Downloads/underworld/img/c9.png)

10. 创建用户，选择是.
 ![10](/home/hd/Downloads/underworld/img/c10.png)

11. 选择是
 ![12](/home/hd/Downloads/underworld/img/c12.png)

12. 输入用户名,share.
 ![13](/home/hd/Downloads/underworld/img/c13.png)

13. 输入密码，abcd1234,点击下一步.
 ![14](/home/hd/Downloads/underworld/img/c14.png)

14. 选择用户目录.
 ![15](/home/hd/Downloads/underworld/img/c15.png)

15. 选择完全访问权限，点击完成.
 ![16](/home/hd/Downloads/underworld/img/c16.png)



#### 配置原始FTP
配置原始节点FTP过程和配置共享FTP过程完全相同，在第5步需要输入原始FTP节点的IP地址，在第６步输入原始FTP的目录,其他步骤完全一致.

#### 配置SFTP
配置原始节点FTP过程和配置共享FTP过程完全相同，在第5步需要输入原始FTP节点的IP地址，在第６步输入原始FTP的目录,在第7部只选择sftp选项.
 ![1](/home/hd/Downloads/underworld/img/s1.png)


FTP和SFTP的安装到此结束．

### 3. 导入数据库脚本   
在这个章节主要是创建平台需要的表空间，用户和表结构，平台需要3个实例.

|实例名称|关联节点|用途|备注|
|---|----|-----|-----|
|metro|管理，调用||
|metrotask|文件下载||
|jsd|调用||
#### 3.1 metro

#### 3.2 metrotask



#　产品安装

## 概述及安装包
 整个平台包含4个安装包，详细情况如下表所示:
 |安装包名|关联节点|大小|备注|
|---|----|-----|-----|
|hdadmin| 管理|60.2MB||
|fbadmin| 文件下载|64.2MB||
|rpc|调用(64)|21.2MB||
|rpc4dll32|调用(32)|20.4MB||

同时，系统部署过程还需要3个插件，如下表所示:
|插件名称欧|关联节点|版本|大小|备注|
|---|----|-----|-----|---|
|Hyperic-Sigar|调用节点|1.6.4|3.35MB|收集系统各项底层信息的工具集|
|jacob|调用节点|1.13|472KB|Jacob 是 JAVA-COM Bridge的缩写，是一个中间件，能够提供自动化访问MS系统下COM组件和Win32 libraries的功能。|
|nircmd|调用节点|2.81|151KB|NirCmd是一套免费的命令列指令，提供许多控制Windows的参数。让你运用命令列的方式，来执行一些动作|

## 插件安装

### 安装Hyperic-Sigar

Hyperic-Sigar需要在两个调用节点(64和32位)同时部署，详细步骤如下:
1. 使用解压缩软件，解压安装包到指定目录，建议选择当前目录.
 ![1](/home/hd/Downloads/underworld/img/h1.png)

2. 复制hyperic-sigar-1.6.4\sigar-bin\lib下的dll（sigar-amd64-winnt.dll或sigar-x86-winnt.dll）到C:\Windows\System32下.
 ![2](/home/hd/Downloads/underworld/img/h2.png)

### 安装jacob

jacob同样需要部署两个调用节点,详细步骤如下:

1. 从jacob安装包解压后得到两个dll：jacob-1.18-x64.dll，jacob-1.18-x86.dll.
 ![1](/home/hd/Downloads/underworld/img/j1.png)

2. jacob-1.18-x64.dll是64位系统使用，jacob-1.18-x86.dll是32位系统使用;请按照节点类型选择相应的dll包复制文件到%JAVA_HOME%\bin\目录下.
 ![2](/home/hd/Downloads/underworld/img/j2.png)

### 安装nircmd

nircmd也需要部署两个调用节点,详细步骤如下:
1. 将nircmd压缩包解压至c:\nircmd-x64:，如下图所示:
 ![1](/home/hd/Downloads/underworld/img/n1.png)

## 安装和配置tomcat

tomcat需要部署在管理，文件下载和调用(32,64)共4个节点分别部署，
1. 解压缩apache-tomcat-7.0.92-windows-x64.rar
 ![1](/home/hd/Downloads/underworld/img/a1.png)

2. 将解压后的apache-tomcat-7.0.92-windows-x64复制到这4个节点的而D盘根目录.

3. 在开始菜单选择运行，键入cmd后回车.
 ![2](/home/hd/Downloads/underworld/img/a2.png)

4. 切换到tomcat安装目录后，输入start.bat启动tomcat服务器,下图界面代表启动成功，成功后不要关闭，否则就关掉了Tomcat.
 ![3](/home/hd/Downloads/underworld/img/a3.png)

5. 测试Tomcat是否启动成功，打开浏览器在地址栏输入http://locathost:8080/ 若出现下图界面，则启动成功.
 ![4](/home/hd/Downloads/underworld/img/a4.png)

6. 修改tomcat日志字符集,使用notepad++打开apache-tomcat-7.0.92-windows-x64\apache-tomcat-7.0.92\conf\logging.properties文件，将第47行UTF-8修改为GB2312，如下如所示:
 ![5](/home/hd/Downloads/underworld/img/x1.png)



## 部署管理节点
1. 解压缩管理节点hdadmin.war包到当前目录.
 ![1](/home/hd/Downloads/underworld/img/g1.png)

2. 将压缩后的haadmin文件夹复制到管理节点tomcat应用文件夹(apache-tomcat-7.0.92-windows-x64\apache-tomcat-7.0.92\webapps)下.
  ![2](/home/hd/Downloads/underworld/img/g3.png)

3. 使用notepad++打hdadmin\WEB-INF\classes\common.properties文件,将FTP修改为指定参数,将checkurl修改为rpc(64位)节点IP地址,如下图所示:
  ![3](/home/hd/Downloads/underworld/img/g2common.png)

4. 使用notepad++打hdadmin\WEB-INF\classes\jdbc.properties文件,修改jdbc连接为metro实例提供的参数,如下图所示:
  ![4](/home/hd/Downloads/underworld/img/g2jdbc.png)

5. 重新启动tomcat服务器，管理节点部署完成.

## 部署调用节点
*需要分别部署32位和64位平台*
 
### 部署64位调用节点

*部署64位调用节点*

1. 解压缩管理节点rpc.war包到当前目录.
  ![1](/home/hd/Downloads/underworld/img/r1.png)

2. 将压缩后的rpc文件夹复制到管理节点tomcat应用文件夹(apache-tomcat-7.0.92-windows-x64\apache-tomcat-7.0.92\webapps)下.

3. 使用notepad++打rpc\WEB-INF\classes\config.properties文件,将FTP,SFTP和jsd实例修改为指定参数如下图所示:
  ![2](/home/hd/Downloads/underworld/img/r2.png)

4. 同时修改regasm_full_path为nircmd安装路径regasm_full_path=C:/nircmd-x64/nircmd.exe elevatecmd runassystem C:/Windows/Microsoft.NET/Framework64/v4.0.30319/RegAsm.exe /codebase ，如下图所示:
　![3](/home/hd/Downloads/underworld/img/r4.png)

5. 使用notepad++打rpc\WEB-INF\classes\jdbc.properties文件,修改jdbc连接为metro实例提供的参数,如下图所示:
  ![4](/home/hd/Downloads/underworld/img/r3.png)

6. 重新启动tomcat服务器，调用节点部署完成.

### 部署32为调用节点

*部署32位调用节点*

 调用节点(32位)部署过程和部署64位完全一致，详细步骤请参考64位调用节点部署.

## 部署文件下载节点
*部署文件下载节点*

1. 解压文件下载节点fbadmin.war包到当前目录.
  ![1](/home/hd/Downloads/underworld/img/w1.png)

2. 将压缩后的fbadmin文件夹复制到管理节点tomcat应用文件夹(apache-tomcat-7.0.92-windows-x64\apache-tomcat-7.0.92\webapps)下.

3. 使用notepad++打fbadmin\WEB-INF\classes\common.properties文件,将FTP和SFTP修改为指定参数．
  ![3](/home/hd/Downloads/underworld/img/w2.png)

4. 使用notepad++打fbadmin\WEB-INF\classes\jdbc.properties文件,修改jdbc连接为metrotask实例提供的参数,如下图所示:
  ![4](/home/hd/Downloads/underworld/img/w3.png)

5. 重新启动tomcat服务器，调用节点部署完成.  

# 常见问题
*安装过程中可能会出现的问题，以及解决方法*
# 首次初始化
*安装完成后的操作*

# 版本升级更新
