### mongodb安装
1. [官方文档](https://docs.mongodb.com/v4.0/tutorial/install-mongodb-on-ubuntu/)
2. 设为开机启动项目
```sh
sudo systemctl enable mongod.service
```
3. 設置用戶、遠程訪問
   - 設置用戶認證
```
    # 啓動shell
    mongo
    # 設置認證用戶
    use admin
    db.createUser(
    {
        user: "root",
        pwd: "password",
        roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ],
        mechanisms : ["SCRAM-SHA-1"]
    }
    )
    # vim /etc/mongod.conf
        security:
            authorization: enabled
    # 重啓服務
```
  - 設置遠程訪問
  ```
  vim /etc/mongod.conf
  bindIp: 0.0.0.0
  ```

### 批量kill进程的shell命令
```
ps -ef | grep chrome | grep -v grep | awk '{ print $2}'|xargs kill -9
```

### 
