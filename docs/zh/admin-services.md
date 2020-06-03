# 服务启停

使用由Websoft9提供的 SqlServer 部署方案，可能需要用到的服务如下：

## SqlServer

```shell
sudo systemctl start sqlserver-server
sudo systemctl stop sqlserver-server
sudo systemctl restart sqlserver-server
sudo systemctl status sqlserver-server

# you can use this debug mode if SqlServer service can't run
sqlserver-server console
```

### MySQL

```shell
sudo systemctl start mysql
sudo systemctl stop mysql
sudo systemctl restart mysql
sudo systemctl status mysql
```

### Redis

```shell
systemctl start redis
systemctl stop redis
systemctl restart redis
systemctl status redis
```