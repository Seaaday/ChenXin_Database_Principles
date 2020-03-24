week5课堂作业-陈鑫.md


mysql> show databases
    -> ;
+--------------------+
| Database           |
+--------------------+
| blcu_db_demo       |
| homework4          |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.00 sec)

mysql> use blcu_db_demo ;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> select * from blcu_db_demo ;
ERROR 1146 (42S02): Table 'blcu_db_demo.blcu_db_demo' doesn't exist
mysql> show blcu_db_demo ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'blcu_db_demo' at line 1
mysql> select * from student;
+-----+--------+------+-----------+-------+
| sno | sname  | ssex | sbirthday | class |
+-----+--------+------+-----------+-------+
| 101 | 李军   | 男   |      1976 | 95033 |
| 103 | 陆君   | 男   |      1974 | 95031 |
| 104 | 尚文   | 男   |      1978 | 95033 |
| 105 | 框明   | 男   |      1975 | 95031 |
| 107 | 王丽   | 女   |      1976 | 95033 |
| 108 | 曾华   | 男   |      1977 | 95033 |
| 109 | 王芳   | 女   |      1977 | 95031 |
+-----+--------+------+-----------+-------+
7 rows in set (0.00 sec)

mysql> select * from student where ssex='男';
+-----+--------+------+-----------+-------+
| sno | sname  | ssex | sbirthday | class |
+-----+--------+------+-----------+-------+
| 101 | 李军   | 男   |      1976 | 95033 |
| 103 | 陆君   | 男   |      1974 | 95031 |
| 104 | 尚文   | 男   |      1978 | 95033 |
| 105 | 框明   | 男   |      1975 | 95031 |
| 108 | 曾华   | 男   |      1977 | 95033 |
+-----+--------+------+-----------+-------+
5 rows in set (0.00 sec)

mysql> select * from student where ssex='女';
+-----+--------+------+-----------+-------+
| sno | sname  | ssex | sbirthday | class |
+-----+--------+------+-----------+-------+
| 107 | 王丽   | 女   |      1976 | 95033 |
| 109 | 王芳   | 女   |      1977 | 95031 |
+-----+--------+------+-----------+-------+
2 rows in set (0.00 sec)

mysql> select * from student order by sbirthday asc;
+-----+--------+------+-----------+-------+
| sno | sname  | ssex | sbirthday | class |
+-----+--------+------+-----------+-------+
| 103 | 陆君   | 男   |      1974 | 95031 |
| 105 | 框明   | 男   |      1975 | 95031 |
| 101 | 李军   | 男   |      1976 | 95033 |
| 107 | 王丽   | 女   |      1976 | 95033 |
| 108 | 曾华   | 男   |      1977 | 95033 |
| 109 | 王芳   | 女   |      1977 | 95031 |
| 104 | 尚文   | 男   |      1978 | 95033 |
+-----+--------+------+-----------+-------+
7 rows in set (0.00 sec)

mysql> select * from student order by sbirthday desc;
+-----+--------+------+-----------+-------+
| sno | sname  | ssex | sbirthday | class |
+-----+--------+------+-----------+-------+
| 104 | 尚文   | 男   |      1978 | 95033 |
| 108 | 曾华   | 男   |      1977 | 95033 |
| 109 | 王芳   | 女   |      1977 | 95031 |
| 101 | 李军   | 男   |      1976 | 95033 |
| 107 | 王丽   | 女   |      1976 | 95033 |
| 105 | 框明   | 男   |      1975 | 95031 |
| 103 | 陆君   | 男   |      1974 | 95031 |
+-----+--------+------+-----------+-------+
7 rows in set (0.00 sec)

mysql> select * from sname where ssname like'王';
ERROR 1146 (42S02): Table 'blcu_db_demo.sname' doesn't exist
mysql> select * from student where sname like'王';
Empty set (0.00 sec)

mysql> select sname from student where sbirthday like '6';
Empty set (0.00 sec)

mysql> select * from student where sname like '王%';
+-----+--------+------+-----------+-------+
| sno | sname  | ssex | sbirthday | class |
+-----+--------+------+-----------+-------+
| 107 | 王丽   | 女   |      1976 | 95033 |
| 109 | 王芳   | 女   |      1977 | 95031 |
+-----+--------+------+-----------+-------+
2 rows in set (0.00 sec)

mysql> exit;
Bye
chenxin@ChendeMacBook-Pro ~ % 