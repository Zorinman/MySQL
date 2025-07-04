# 1.索引数据结构
都是B+树
但是

## InnoDB
**主键是聚簇索引，辅助键是非聚簇索引**，
主键的聚簇索引中B+ 树的`叶子节点存储的是主键ID索引和实际的数据`。
辅助键的非聚簇索引，B+ 树`叶子节点存储的是索引和数据的地址`，但可以通过覆盖索引这种技术手段实现非聚簇索引不需要回表，直接索引实际数据。

![alt text](图片/image-3.png)
### 物理文件
创建一个，表，表名为student_innodb
![alt text](图片/image.png)

可以看到有两个存储文件
`.frm`:
.frm文件是一份定义文件，也就是定义student_innodb表的结构，是一张怎么样的表
`.ibd`:
.ibd文件则是该表的索引，数据存储文件，既该表的所有索引树，所有行记录数据都存储在该文件中

## MyISAM 

**主键和辅助键索引都是非聚簇索引**，B+ 树`叶子节点存储的是索引和数据的地址`，它的`索引和实际数据是分开的`

![alt text](图片/image-2.png)

### 物理文件
创建一个名为student_myisam的表
![alt text](图片/image-1.png)
可以看到有三个存储文件
`.frm`：表定义文件,与InnoDB一致
`.MYD`：MYD文件是MyISAM存储引擎表的所有行数据的文件
`.MYI`：MYI文件存放的表的索引信息

# 2 InnoDB有日志机制，redolog可以支持安全恢复，MyISAM无日志机制不支持崩溃后的安全恢复

# 3 InnoDB支持事务，MyISAM不支持事务，
InnoDB实现了四种标准的隔离级别，利用MVCC来支持高并发，默认事务隔离级别为可重复读，支持行锁，利用行锁+间隙锁提供可重复读级别下防止幻读的能力

# 4. InnoDB支持外键，MyISAM不支持


# 使用场景
1. **InnoDB优势场景**

**高并发读写**：OLTP系统如电商订单、金融交易
**数据强一致**：需要事务支持的支付系统
**复杂查询**：通过行锁减少锁冲突，支持高频更新

2. **MyISAM适用场景**
**读密集型操作**：数据仓库、报表分析（OLAP）
**静态数据管理**：CMS内容管理、历史日志归档