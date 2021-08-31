# 1、索引的本质

索引是帮助MySQL高效获取数据的**排好序**的**数据结构**。

索引的数据结构有：

1. 二叉树：根节点左边比根节点小，右边比根节点大，最差的情况下会退化成链表
2. 红黑树：自平衡二叉查找树
3. hash表：用hash表存储数据
  1. 对索引的key进行一次hash计算就可以定位出数据存储的位置
  2. 很多时候Hash索引比B+Tree 索引更高效
  3. 仅能满足 "=" 、 "IN"，不支持范围查询
  4. hash冲突问题
4. B-Tree：平衡多路查找树
   - 叶节点具有相同的深度，叶节点的指针为空
   - 所有索引元素不重复
   - 节点中的数据索引从左到右递增排列

![索引](E:\学习笔记\img\B-Tree.png)

- B+Tree：B-Tree的优化
  1. 非叶子节点不存储data，只存储索引（冗余），可以放更多的索引。
  2. 叶子节点包含所有索引字段。
  3. 叶子节点用指针连接，提高区间访问性能。

![索引](E:\学习笔记\img\B+Tree.png)

> B+Tree相对于B-Tree的区别:
>
> 1. 非叶子节点只存储键值信息。
> 2. 所有叶子节点之间都有一个链指针。
> 3. 数据记录都存放在叶子节点中。

查看innodb的叶子节点大小

```mysql
SHOW GLOBAL STATUS like 'Innodb_page_size';
```

![image-20210820140409266](E:\学习笔记\img\mysql叶子节点大小.png)

# 2.InnoDB索引

- 表数据文件本身就是按照B+Tree组织的一个索引结构文件。
- 聚集索引-叶节点包含了完整的数据记录。
- InnoDB的主键索引使用的聚集索引。其他的非主键索引的数据储存的是主键值，非主键查询的话需要回表，也就是先查到主键，再到主键索引中去查数据。
- 如果没有创建主键的话，会在表中查找一个数据独一无二的列作为主键，建立聚集索引，如果没有这种特殊的列的话，会创建一个隐藏的列作为聚集索引。

![image-20210820211117123](E:\学习笔记\img\MySQL-InnoDB-聚集索引.png)

> 聚集索引：数据记录和索引在同一个文件中。（InnoDB）
>
> 非聚集索引：索引文件和数据文件是分离的。（MyISAM）

## 3、索引最左前缀原则

查询需要根据创建联合索引时候的顺序查找

```mysql
	KEY 'idx_name_age_position'('name','age','position') USING BTREE
	
	EXPLAIN SELECT * FROM employees WHERE name = 'Bill' AND age = 31;
	EXPLAIN SELECT * FROM employees WHERE age = 30 AND position = 'dev'; 
	EXPLAIN SELECT * FROM employees WHERE position = 'manager';
```

只有第一条查询语句会走索引，因为联合索引是根据创建的顺序进行排序的。

如果不从按顺序查询的话，其他的索引不一定是排好序的。比如第二个，直接查询30的话可以看出，后面的数据中age还有30的，无法进行准备

![image-20210822172245982](C:\Users\80463\AppData\Roaming\Typora\typora-user-images\image-20210822172245982.png)