# SQL Server2017 Notes

组件名称：SQLServer
安装文档：https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-2017
配置文档: https://docs.microsoft.com/en-us/sql/linux/sample-unattended-install-ubuntu?view=sql-server-linux-2017
支持平台： Debian家族 | RHEL家族 | Windows |k8s |Docker  

责任人：zxc

## 概要

SQL Server是由Microsoft开发和推广的关系数据库管理系统。

## 环境要求

* 程序语言： C#  ASP.NET  T-SQL
* 应用服务器：自带
* 数据库：SQL Server
* 依赖组件：
* 其他：

## 安装说明

本项目采用官方yum源安装。


下面基于不同的安装平台，分别进行安装说明。

### Ubuntu(ubuntu16.04 ,ubuntu18.04)

```shell
#安装SQL Server服务器
# 导入存储库密钥
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# 注册微软 SQL Server ubuntu存储库(此命令也可用于注册2019版本)
sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2017.list)" 

#安装SQL Server
sudo apt-get update
sudo apt-get install -y mssql-server



#安装SQL Server命令行工具(sqlcmd和bcp)

#导入公钥
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

#注册微软存储库
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list

#更新源列表并安装ODBC驱动
sudo apt-get update 
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev

#sql Server开机自启
systemctl daemon-reload
systemctl enable mssql-server.service
#本地连接
sqlcmd -S localhost -U SA -P '<YourPassword>'
```

## 路径

* 程序路径：/opt/mssql/bin/sqlservr
* 日志路径: /var/opt/mssql/data/下的 mastlog.ldf  modellog.ldf  msdblog.ldf  templog.ldf
* 配置文件路径：/opt/mssql/lib/mssql-conf
* 其他...

##配置
#配置SQL Server
sudo MSSQL_SA_PASSWORD='<YourPassword>' \
     MSSQL_PID='express' \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

## 账号密码


### 数据库密码

如果有数据库  


* 数据库安装方式：
* 账号密码： SA | <YourPassword>

### 后台账号 

无
如果有后台账号

* 登录地址 
* 账号密码   
* 密码修改方案：最好是有命令行修改密码的方案

## 服务

本项目安装后自动生成：couchbase-server.service

备注：本项目安装后自动生成服务

服务文件位置：/lib/systemd/system/mssql-server.service

```
[Unit]
Description=Microsoft SQL Server Database Engine
After=network.target auditd.service
Documentation=https://docs.microsoft.com/en-us/sql/linux

[Service]
ExecStart=/opt/mssql/bin/sqlservr
User=mssql
WorkingDirectory=/var/opt/mssql

# Kill root process
KillMode=process

# Wait up to 30 seconds for service to start/stop
TimeoutSec=30min

# Remove process, file, thread limits
#
LimitNPROC=infinity
LimitNOFILE=infinity
TasksMax=infinity
UMask=007

# Restart on non-successful exits.
Restart=on-failure

# Don't restart if we've restarted more than 3 times in 2 minutes.
StartLimitInterval=120
StartLimitBurst=3

[Install]
WantedBy=multi-user.target

```

## 环境变量(可选择,建议选择交互式会话)

#使sqlcmd/bcp可非交互式会话
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
source ~/.bash_profile

#使sqlcmd/bcp可交互式会话
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc

## 版本号

通过如下的命令获取主要组件的版本号: 

```
# Check  SQLServer version
sqlcmd -S localhost -U SA -P '<YourPassword>'(连接上服务器)
1> select @@version
2> GO  
```

## 常见问题

#### 有没有管理控制台？

无

#### 本项目需要开启哪些端口？

| item      | port |
| --------- | ---- |
| sqlserver | 1433 |


#### 有没有CLI工具？

有,mssql-cli(命令行查询工具) 和sqlcmd 


## 日志

* 2020-05-12完成ubuntu安装研究