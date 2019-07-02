用于运行Oracle Database 11g Standard / Enterprise的映像。由于oracle许可证限制，映像不包含数据库本身，并将在首次运行时从外部目录安装它。

``此镜像仅供开发使用``

＃用法
从[Oracle站点]下载数据库安装文件（http://www.oracle.com/technetwork/database/in-memory/downloads/index.html）并将其解压缩到** install_folder **。
运行容器，它将安装oracle并创建数据库：

```SH
docker run --privileged --name oracle11g -p 1521:1521 -v <install_folder>:/install jinghongbo/oracle-11g
```
然后你可以提交这个容器来安装和配置oracle数据库：
```SH
docker commit oracle11g oracle11g-installed
```

数据库位于** /opt/oracle **文件夹中

OS用户：
* root / install
* oracle / install

数据库用户：
* SYS / oracle

您可以选择将dpdump文件夹映射到简单的上载转储：
```SH
docker run --privileged --name oracle11g -p 1521:1521 -v <install_folder>:/ install -v <local_dpdump>:/opt/oracle/dpdump jinghongbo/ oracle-11g
```
要执行impdp / expdp，只需使用docker exec命令：
```SH
docker exec -it oracle11g impdp ..
```
