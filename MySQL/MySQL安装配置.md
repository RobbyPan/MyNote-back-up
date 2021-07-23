## MySQL安装配置

1. Mysql的官网-->https://www.mysql.com/，下载社区版

2. 配置环境变量，path新建bin目录地址

3. bin文件夹所在目录下新建mysql配置文件 my.ini

   ```
   [mysqld]
   basedir=D:\....\
   datadir=D:\....\data\
   port=3306
   skip-grant-tables  //跳过密码验证
   ```

   

4. 管理员CMD进入bin 执行`mysqld --install`

5. `mysqld --initialize`

6. `net start mysql`

7. `mysql -u root -p`  不输入密码

8. `ALTER USER "root"@"localhost" IDENTIFIED  BY "123456";`修改密码

9. `flush privileges;`刷新权限

10. 退出再重启mysql服务即可





