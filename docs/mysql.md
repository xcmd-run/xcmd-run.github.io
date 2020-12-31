# MySQL 8.0

## 安装
### rpm install
1. 下载安装包 https://dev.mysql.com/downloads/mysql/
2. ```
   wget https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-community-server-8.0.21-1.el7.x86_64.rpm
   mysql-community-common-8.0.21-1.el7.x86_64.rpm
   mysql-community-libs-8.0.21-1.el7.x86_64.rpm
   mysql-community-client-8.0.21-1.el7.x86_64.rpm
   ```
3. sudo yum install mysql-community-server-8.0.21-1.el7.x86_64.rpm
4. yum repolist enabled | grep "mysql.*-community.*"
5. sudo yum module disable mysql
6. sudo yum install mysql-community-server
7. sudo service mysqld start
8. sudo service mysqld status
9. sudo grep 'temporary password' /var/log/mysqld.log
10. ```
    mysql -uroot -p
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'A1b2C#d4E%';
    ```

### docker install
1. docker pull mysql/mysql-server:8.0.21
2. ```
   docker run --name=mysql --restart on-failure -d mysql/mysql-server:8.0.21
    ```
    ```
    docker run --name mysql -p 3306:3306 -d -e MYSQL_ROOT_PASSWORD=A1b2C#d4E% --mount type=bind,src=/opt/mysql/my.cnf,dst=/etc/my.cnf --mount type=bind,src=/opt/mysql/data,dst=/var/lib/mysql mysql/mysql-server:8.0.21
    ```
3. docker logs mysql
4. docker logs mysql 2>&1 | grep GENERATED
5. docker exec -it mysql mysql -uroot -p
6. ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
7. docker exec -it mysql bash
8. ls /var/lib/mysql

## 常用命令
1. 连接： ` mysql -h host -u user -p `
2. 查看版本 `SELECT VERSION(), NOW();`
3. 查看数据库 `SHOW DATABASES;`
4. 创建数据库 `CREATE DATABASE test;`
5. 使用数据库 `USE test;`
6. 查看表 `SHOW TABLES;`
7. 创建表 `CREATE TABLE pet (name VARCHAR(20), owner VARCHAR(20), species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);`
8. 查看表结构 `DESCRIBE pet;`
    ```
    +---------+-------------+------+-----+---------+-------+
    | Field   | Type        | Null | Key | Default | Extra |
    +---------+-------------+------+-----+---------+-------+
    | name    | varchar(20) | YES  |     | NULL    |       |
    | owner   | varchar(20) | YES  |     | NULL    |       |
    | species | varchar(20) | YES  |     | NULL    |       |
    | sex     | char(1)     | YES  |     | NULL    |       |
    | birth   | date        | YES  |     | NULL    |       |
    | death   | date        | YES  |     | NULL    |       |
    +---------+-------------+------+-----+---------+-------+
    6 rows in set (0.00 sec)
    ```
9. load数据 `LOAD DATA LOCAL INFILE '/path/pet.txt' INTO TABLE pet;`
    ```
    Whistler        Gwen    bird    \N      1997-12-09      \N
    ```
    ```
    SHOW GLOBAL VARIABLES LIKE 'local_infile';
    +---------------+-------+
    | Variable_name | Value |
    +---------------+-------+
    | local_infile  | OFF   |
    +---------------+-------+
    1 row in set (0.00 sec)

    my.cnf 
    local_infile=1
    service mysql restart
    mysql -uroot -p --local_infile=1

    load data local infile '/opt/pet.txt' into table pet;   
    Query OK, 1 row affected, 6 warnings (0.02 sec)
    Records: 1  Deleted: 0  Skipped: 0  Warnings: 6

    show warnings limit 10
    ```
10. 写入数据 `INSERT INTO pet VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);`
11. 修改数据 `UPDATE pet SET birth = '1989-08-31' WHERE name = 'Bowser';`
12. 查询数据 `SELECT name, birth,CURDATE(),TIMESTAMPDIFF(YEAR,birth,CURDATE()) AS age FROM pet WHERE birth >= '1998-1-1' ORDER BY birth DESC;`
13. 删除数据 `DELETE FROM test WHERE name='Bowser';`
14. 查看当前数据库 `SELECT DATABASE();`
15. 查看数据库中的表 `SHOW TABLES;`
16. 批量执行 `mysql -h host -u user -p ******** < batch-file > mysql.out`
17. 自定义变量
    ```
    SELECT @min_price:=MIN(price),@max_price:=MAX(price) FROM shop;
    SELECT * FROM shop WHERE price=@min_price OR price=@max_price;
    ```
18. 显示建表语句 ` SHOW CREATE TABLE pet \G;`
    ```
    *************************** 1. row ***************************
            Table: pet
        Create Table: CREATE TABLE `pet` (
          `name` varchar(20) DEFAULT NULL,
          `owner` varchar(20) DEFAULT NULL,
          `species` varchar(20) DEFAULT NULL,
          `sex` char(1) DEFAULT NULL,
          `birth` date DEFAULT NULL,
          `death` date DEFAULT NULL
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
        1 row in set (0.00 sec)
    ```

## MySQL程序
- mysqld MySQL守护进程
- mysqld_safe mysqld启动脚本
- mysql.server 服务启动脚本，系统服务调用脚本启动数据库
- mysqld_multi 启动和停止多个服务器的脚本
- comp_err 构建和安装过程中的错误日志
- mysql_secure_installation 提搞安装的安全性
- mysql_ssl_rsa_setup ssl配置脚本
- mysql_tzinfo_to_sql 加载时区信息
- mysql_upgrade mysql升级程序
- mysql MySQL命令行工具
- mysqladmin 命令行管理工具
- mysqlcheck 表维护,检查,维修,分析,优化表
- mysqldump 数据导出工具
- mysqlimport 数据导入工具
- mysqlpump 导出数据SQL
- mysqlsh 高级客户端和代码编辑器
- mysqlshow 显示数据库信息 数据库、表、列、索引
- mysqlslap mysql监控工具
- innochecksum InnoDB 离线校验工具
- myisam_ftdump MyISAM 全文索引信息工具
- myisamchk MyISAM 表工具
- myisamlog MyISAM 日志工具
- myisampack MyISAM 压缩工具
- mysql_config_editor 
- mysqlbinlog binlog 工具
- mysqldumpslow 慢查询日志工具
- mysql_config 
- my_print_defaults 
- lz4_decompress LZ4 解压工具
- perror 系统错误或错误码查询工具
- zlib_decompress zlib 解压工具

## MySQL程序参数
### 命令行参数
- 使用 `-` 或 `--` 来指定参数，`-` 缩略名，`--` 全名，例如 `-h localhost`, `--host=localhost`
- 参数名大小写敏感
- `-` 参数和值直接可以使用空格分隔，也可以不使用空格比如`-h localhsot`、`-hlocalhost`, `--` 参数和值直接使用`=`分隔。
```bash
# 密码test
mysql -ptest  
# 密码需要确认，test为数据库
mysql -p test
```
- 参数名中的 `-` 和`_`是等效的，如：`--skip-grant-tables`、`--skip_grant_tables `

### 文件参数
|文件 | 用途|
|--  | --
|/etc/my.cnf	        |Global options|
|/etc/mysql/my.cnf	    |Global options|
|SYSCONFDIR/my.cnf	    |Global options|
|$MYSQL_HOME/my.cnf	    |Server-specific options (server only)|
|defaults-extra-file	|The file specified with `--defaults-extra-file`, if any|
|~/.my.cnf	            |User-specific options |
|~/.mylogin.cnf	        |User-specific login path options (clients only)|
|DATADIR/mysqld-auto.cnf	|System variables persisted with SET PERSIST or SE PERSIST_ONLY (server only)|


### 命令行连接服务器



## 读写分离、高可用
### MaxScale

### ProxySQL
