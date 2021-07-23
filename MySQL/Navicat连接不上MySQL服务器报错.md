## Navicat连接不上MySQL服务器报错

由于navicat版本的问题造成连接失败。mysql8之前的版本中加密规则是mysql_native_password，而在mysql8之后，加密规则则是caching_sha2_password

#### 解决

进入mysql `mysql -u root -p`

输入`ALTER USER 'root'@'localhost' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;` password替换为mysql连接密码

输入`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';`修改新的密码

刷新权限，使生效`FLUSH PRIVILEGES; `

