#本库非官方，个人分流，如需详细教程及安装包请访问官网

#官网：https://goedge.cn/downloads

#安装管理平台

可以选择使用edge-boot或者手动安装。

系统需求

最小需求：

操作系统：Linux

CPU不少于1核心

可用内存不少于1G

可用硬盘空间不小于10G

对于每日千万访问以上的CDN系统推荐配置如下：

CPU不少于8核心

可用内存不少于8G

可用硬盘空间不小于200G

准备工作

在安装GoEdge之前，需要你做以下准备工作：

安装一个或者使用现有的 MySQL 5.7.8/MySQL 8.0 以上版本；如果你会一些Linux基本命令，但是不知道怎么安装MySQL，可以参考这里 安装MySQL；另外请注意：
安装使用的MySQL用户密码不能为空

当前只支持通过端口连接MySQL，不能使用Sock文件连接

手动安装时，Linux服务器需要确认有 unzip 命令，用来解压压缩包，可以使用：

unzip
命令来确认这个命令是否可用，如果提示command not found，可以参考 安装unzip 一文来安装。

安装方式1：使用脚本快速安装

可以使用install.sh快速安装GoEdge管理平台，目前仅限于Linux系统；在你的系统上运行以下命令：

sudo sh -c "$(wget https://goedge.cn/install.sh -O -)"

运行后，如果遇到域名解析或者网络问题，请再次尝试执行；如果出现：

started ok
please open the url http://SERVER_IP:7788 on your browser

这样的提示，说明已经安装成功；默认的安装目录为/usr/local/goedge/edge-admin；安装后，在浏览器上访问：

http://IP地址:7788/

即可进入安装界面，其中IP地址是你服务器的IP地址；如果服务器有安全策略或者防火墙，需要放行7788端口。

使用脚本安装后，系统会自动安装edge-boot，之后可以使用edge-boot管理GoEdge相关应用。

安装方式2：使用edge-boot安装

可以使用EdgeBoot简单安装管理平台，EdgeBoot下载地址：

EdgeBoot 通用版本

国内地址：https://dl.goedge.cn/edge-boot/linux/amd64/edge-boot

海外地址：https://global.dl.goedge.cn/edge-boot/linux/amd64/edge-boot

EdgeBoot ARM64版本

国内地址：https://dl.goedge.cn/edge-boot/linux/arm64/edge-boot

海外地址：https://global.dl.goedge.cn/edge-boot/linux/arm64/edge-boot

在服务器上下载此文件，放到任何目录下都可以（建议放到 /usr/local/bin/ 目录下，这样可以在任何地方直接执行edge-boot，不需要输入目录），然后执行：

 使用wget下载

  你需要把引号里面的内容替换成上面的对应版本的下载地址

wget "上面的EdgeBoot下载地址"

  第一次运行时，需要修改此文件为可执行

  ./edge-boot 表示在当前目录下，你如果放到了别的目录，需要指定edge-boot完整的路径名

chmod u+x ./edge-boot

  国内用户用这个

./edge-boot install admin 

 海外用户增加参数--g，可以从海外线路下载，edge-boot版本需要在v1.1.0以上

./edge-boot install admin --g

即可安装，默认的安装目录为/usr/local/goedge/edge-admin；安装后，在浏览器上访问：

http://IP地址:7788/

即可进入安装界面，其中IP地址是你服务器的IP地址；如果服务器有防火墙或者安全策略，需要放行7788、8001 端口。

如果需要升级，可以执行：

./edge-boot upgrade admin

如果没有安装MySQL数据库，可以使用：

./edge-boot install mysql

此命令只适用于CentOS/Redhat，安装后的数据库数据默认目录为 /var/lib/mysql。

安装方式3：手动安装

在官网下载对应版本的安装压缩包

上传到你的服务器上，建议放到 /usr/local/goedge/目录下，然后使用unzip解压，类似于：

cd $安装压缩包所在目录

unzip -o ./edge-admin-linux-amd64-v0.4.7.zip

把其中的v0.4.7换成实际的版本号；

启动管理平台：

cd edge-admin/

bin/edge-admin start

如果没有意外的话，服务就正常启动了，并提示类似于以下的信息：

Edge Admin started ok, pid: 109053

可以使用ps命令，来检查进程是否存在：

ps ax|grep edge

可以看到类似于以下的进程信息：

31643 ?        Sl     0:04 bin/edge-admin

就说明管理平台启动成功；

可以在 logs/run.log 中查看启动的日志，方便我们诊断问题；

默认启动的端口是 7788，确认进程已经启动的时候，可以在浏览器上通过：

http://IP地址:7788/

访问管理平台；如果你的服务器上已经设置了防火墙，需要在防火墙设置 7788 这个端口是通过的；

如果能正常访问上述网址的话，系统会自动进入安装过程，按照界面提示填写各项选项即可。

安装方式4：使用Docker安装

请参考 使用Docker安装 一节内容。

安装界面

介绍

这一步用于简要介绍Edge的安装界面。

设置API节点

设置API节点

这一步用于选择API节点，API节点用于作为系统的多个组件之间通讯的桥梁，如果你以前没有安装过GoEdge，建议选择”自动启动新API节点”，这样系统会自动在本地（即和管理平台一个服务器）启动一个新的API节点，而不需要另外重新安装。
选项说明：

节点端口：选一个在1024-65535之间并且没有正在使用的端口作为要启动的节点端口。如果你的服务器上有防火墙，请一定记得设置这个端口为通过，这样将来部署在别的服务器上的边缘节点才可以访问。默认为 8001，注意检查这个端口有没有被别的进程所占用。

节点主机地址：其他节点访问此API节点的主机地址，可以是IP或者域名，第一次安装时通常是 当前服务器 的IP地址。我们提供了对应的管理界面，安装完成后，可以随时修改这个地址。
设置MySQL数据库


如果是安装的MySQL和管理平台是在同一台服务器上，主机地址通常可以填写为127.0.0.1。

不建议使用公网地址的MySQL地址，既不安全，又可能因为防火墙等原因被拒绝访问。

设置管理员账号


可以设置稍微复杂的管理员账号，但请一定要记住这个密码。

完成安装

这一步可以确认前面所填写的信息，如果确认无误后，可以点击”确认并开始安装”，这一步骤需要的时间较长，需要耐心等待几秒钟。

安装完成

如果安装过程中没有错误产生的话，会出现以上的界面，点击”确定”按钮即可进入登录界面。

如果出现了错误，请截图发给我们，我们会随时帮助你诊断问题所在。

安装系统服务

在安装完成后可以使用：

cd $EdgeAdmin安装目录

bin/edge-admin service

命令安装systemd系统服务，这样在系统重启后，可以自动启动服务。

使用EdgeBoot自动安装的安装目录为 /usr/local/goedge/edge-admin

常见问题

更多常见问题参考常见问题一节。

安装后在浏览器上无法访问7788端口

通常是安全策略或者防火墙没有放行7788端口所致，请修改相应配置。

RPC错误

如果类似于以下的错误：

rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing dial tcp 192.168.2.30:8001: connect: connection refused"

可能的原因：

API节点启动失败，请查看 edge-admin/edge-api/logs/run.log 查看错误日志；

API节点的IP地址和端口不能被正常访问，可以检查API节点是否启动（即edge-api进程是否正常运行），IP和防火墙和其他安全策略设置是否正确。

无法完成安装，一直停留在安装界面


可能有以下原因：

可能因为你的服务器有安全策略或者有防火墙，导致系统无法连接你设置的API节点端口，请把在安装过程中设置的API节点端口在安全策略和防火墙中都设置允许通过，然后再重新进入安装界面进行安装。

你的数据库连接和传输数据过慢，导致安装过程超时，请使用本地数据库或者在同一个局域网里的数据库。

无法登录系统，一直停留在登录界面

登录正确的账号和密码，但是登录不了，一直停留在登录界面，类似于以下界面：

安装完成

原因：你在同一个域名或IP下曾经使用HTTPS协议登录过系统，所以系统自动屏蔽了HTTP协议访问 解决方法：改成HTTPS协议登录，或者清除这个域名下的所有Cookie重新登录。

重启操作系统的时候没有跟着启动

请参考本文 安装系统服务 一节内容安装系统服务。

无法通过空密码连接到MySQL/MariaDB

在MySQL/MariaDB安装后，可能会无法通过默认生成的空密码连接，此时你可以创建一个新用户或者修改用户密码后再试。

修改默认密码：

ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';

创建用户：

CREATE USER 'edges'@'localhost' IDENTIFIED BY '123456';

GRANT ALL PRIVILEGES ON 数据库名.* TO 'edges'@'localhost';
