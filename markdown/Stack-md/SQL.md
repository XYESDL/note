# 数据库

[全栈教程-数据库](https://pdai.tech/md/db/sql/sql-db.html)

## 主流关系数据库

1. 商用数据库，例如：Oracle，SQL Server，DB2等
2. 开源数据库，例如：MySQL，PostgreSQL等
3. 桌面数据库，以微软Access为代表，适合桌面应用程序使用
4. 嵌入式数据库，以Sqlite为代表，适合手机应用和桌面程序

## 可视化工具

[Navicat](https://www.navicat.com.cn/)

[TablePlus](https://tableplus.com/)

## 语法

终端登录
```vue
mysql -u root -p
```
SQL是结构化查询语言的缩写，用来访问和操作数据库系统。

表行（Record），列（Column）

关系数据库通过外键可以实现一对多、多对多和一对一的关系。外键既可以通过数据库来约束，也可以不设置约束，仅依靠应用程序的逻辑来保证。

库操作

|说明|语法|
|:----|:---|
|查看所有|SHOW DATABASES;|
|创建|CREATE DATABASE test;|
|删除|DROP DATABASE test;|
|选择|USE test;|
|退出|EXIT;|

权限

|说明|语法|
|:----|:---|
|创建用户|CREATE USER 'username'@'host' IDENTIFIED BY 'password';|
|授权|GRANT permissions ON database.table TO 'username'@'host';|
|撤销权限|REVOKE permissions ON database.table FROM 'username'@'host';|
|修改密码|SET PASSWORD FOR 'username'@'host' = PASSWORD('new_password');|
|查看当前用户|SELECT USER();|
|刷新权限|FLUSH PRIVILEGES;|

表操作

|说明|语法|
|:----|:---|
|列出表|SHOW TABLES;|
|查看表结构|DESC table_name; 或 SHOW COLUMNS FROM table_name;|
|创建表|CREATE TABLE table_name (column1 datatype, column2 datatype);|
|删除表|DROP TABLE table_name;|
|删除字段|ALTER TABLE 表名 DROP COLUMN 字段名;|
|插入数据|INSERT INTO table_name (column1, column2) VALUES (value1, value2);|
|查询数据|SELECT column1, column2 FROM table_name WHERE condition;|
|更新数据|UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;|
|删除数据|DELETE FROM table_name WHERE condition;|

```vue
表新增一列birth，使用：
ALTER TABLE students ADD COLUMN birth VARCHAR(10) NOT NULL;

修改birth列，列名改为birthday，类型改为VARCHAR(20)：
ALTER TABLE students CHANGE COLUMN birth birthday VARCHAR(20) NOT NULL;

删除列：
ALTER TABLE students DROP COLUMN birthday;
```

### 主外键

主键是关系表中记录的唯一标识。主键的选取非常重要：主键不要带有业务含义，而应该使用BIGINT自增或者GUID类型。主键也不应该允许NULL。

```vue
定义外键
ALTER TABLE students
ADD CONSTRAINT fk_class_id
FOREIGN KEY (class_id)
REFERENCES classes (id);

删除外键
ALTER TABLE students
DROP FOREIGN KEY fk_class_id;

自增ID
AUTO_INCREMENT 表示该字段会自动递增
PRIMARY KEY 通常和自增字段一起用，保证唯一性。
```

外键约束的名称fk_class_id可以任意，FOREIGN KEY (class_id)指定了class_id作为外键，REFERENCES classes (id)指定了这个外键将关联到classes表的id列（即classes表的主键）

索引是关系数据库中对某一列或多个列的值进行预排序的数据结构。通过使用索引，可以让数据库系统不必扫描整个表，而是直接定位到符合条件的记录，这样就大大加快了查询速度。

```vue
创建复合索引
ALTER TABLE students
ADD INDEX idx_score (name,score);

唯一索引
ALTER TABLE students
ADD UNIQUE INDEX uni_name (name);

唯一约束
ALTER TABLE students
ADD CONSTRAINT uni_name UNIQUE (name);

查看索引
SHOW INDEX FROM table_name;
```
### 查询
```vue
基本查询

-- 查询:
SELECT * FROM <表名>

-- 条件查询:
SELECT * FROM <表名> WHERE <条件表达式>

-- 投影查询，列名重命名(score重命名为points):
SELECT id, score points, name FROM students;
```

```vue
排序

-- 按score从低到高(默认的排序规则是ASC：“升序”,可以省略):
SELECT id, name, gender, score FROM students ORDER BY score;

-- 按score从高到低:
SELECT id, name, gender, score FROM students ORDER BY score DESC;

-- 先score, 后gender排序:
SELECT id, name, gender, score FROM students ORDER BY score DESC, gender;
```

```vue
分页查询

-- 查询第1页(对结果集从0号记录开始，最多取3条):
SELECT id, name, gender, score
FROM students
ORDER BY score DESC
LIMIT 3 OFFSET 0;

-- 使用聚合查询(多少条记录):
SELECT COUNT(*) FROM students;

-- 使用聚合查询并设置WHERE条件:
SELECT COUNT(*) boys FROM students WHERE gender = 'M';

-- 使用聚合查询计算男生平均成绩:
SELECT AVG(score) average FROM students WHERE gender = 'M';

-- 按class_id分组:
SELECT COUNT(*) num FROM students GROUP BY class_id;
```

### CRUD

```vue
INSERT(一次性添加多条记录，每组值用逗号,分隔):
INSERT INTO <表名> (字段1, 字段2) VALUES (值1, 值2);

UPDATE：
UPDATE <表名> SET 字段1=值1, 字段2=值2 WHERE;

DELETE：
DELETE FROM <表名> WHERE;
```

```vue
插入或替换

使用REPLACE语句，这样就不必先查询，再决定是否先删除再插入：
REPLACE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
若id=1的记录不存在，REPLACE语句将插入新记录，否则，当前id=1的记录将被删除，然后再插入新记录。

插入或更新

插入一条新记录（INSERT），但如果记录已经存在，就更新该记录，此时，可以使用INSERT INTO ... ON DUPLICATE KEY UPDATE ...语句：
INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99) ON DUPLICATE KEY UPDATE name='小明', gender='F', score=99;
若id=1的记录不存在，INSERT语句将插入新记录，否则，当前id=1的记录将被更新，更新的字段由UPDATE指定。

插入或忽略

插入一条新记录（INSERT），但如果记录已经存在，就啥事也不干直接忽略，此时，可以使用INSERT IGNORE INTO ...语句：
INSERT IGNORE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
若id=1的记录不存在，INSERT语句将插入新记录，否则，不执行任何操作。

快照

对一个表进行快照，即复制一份当前表的数据到一个新表，可以结合CREATE TABLE和SELECT：
对class_id=1的记录进行快照，并存储为新表students_of_class1:
CREATE TABLE students_of_class1 SELECT * FROM students WHERE class_id=1;
新创建的表结构和SELECT使用的表结构完全一致。

写入查询结果集

查询结果集需要写入到表中，可以结合INSERT和SELECT，将SELECT语句的结果集直接插入到指定表中。
创建一个统计成绩的表statistics，记录各班的平均成绩：
CREATE TABLE statistics (
    id BIGINT NOT NULL AUTO_INCREMENT,
    class_id BIGINT NOT NULL,
    average DOUBLE NOT NULL,
    PRIMARY KEY (id)
);
用一条语句写入各班的平均成绩：
INSERT INTO statistics (class_id, average) SELECT class_id, AVG(score) FROM students GROUP BY class_id;
确保INSERT语句的列和SELECT语句的列能一一对应，就可以在statistics表中直接保存查询的结果：

强制使用指定索引

使用FORCE INDEX强制查询使用指定的索引。
SELECT * FROM students FORCE INDEX (idx_class_id) WHERE class_id = 1 ORDER BY id DESC;
指定索引的前提是索引idx_class_id必须存在。
```