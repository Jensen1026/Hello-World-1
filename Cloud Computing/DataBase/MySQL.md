# MySQL

- [官方教程](https://dev.mysql.com/doc/refman/8.0/en/)

- 快速教程

  - 创建数据库

    ```mysql
    show databases;（注意末尾有分号）	可以查看当前MySQL中的数据库列表；
    create database test；	创建数据库test；
    use test;	可以进入test数据库（前提是要有此数据库）；
    show tables;	可以查看test数据库中的所有表
    quit	可以退出MySQL的操作管理界面。
    ```

  - 创建表删除表

    ```mysql
    use test;
    create table student(
    id integer,
    name varchar(8)
    password varchar(20));
    ```

    ```mysql
    drop table table_name；	删除一张表。
    ```

  - 修改表名

    ```mysql
    alter table old_name rename to new_name	更改数据表名；
    rename table old_name to new_name	更改数据表名，低版本的MySQL中，已经被删掉。
    ```

  - 增、删、改

    ```mysql
    alter table table_name add column_name column_type	为数据表增加字段；
    alter table table_name change column_name new_column_name new_column_name_type	语句来修改数据表字段名称；
    alter table table_name drop column_name	来删除数据表字段。
    ```

## 