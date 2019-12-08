# MySQL

### 目录

1. [Engine（数据库引擎）](#engine数据库引擎)
    1. [ISAM](#isam)
    1. [MyISAM](#myisam)
    1. [InnoDB](#innodb)
    1. [HEAP（MEMORY）](#heapmemory)
    1. [MyISAM与InnoDB的区别](#myisam与innodb的区别)
    1. [参考](#参考)
1. [CREATE TABLE](#create-table)
    1. [AUTO_INCREMENT](#auto_increment)
    1. [CURRENT_TIMESTAMP](#current_timestamp)
    1. [参考](#参考-1)

### Engine（数据库引擎）

  #### ISAM
  
  > `ISAM`是一个定义明确且**历经时间考验的数据表格管理方法**，它在设计之时就考虑到数据库被查询的次数要远大于更新的次数。因此，`ISAM`执行**读取操作的速度很快，而且不占用大量的内存和存储资源**。`ISAM`的**两个主要不足之处在于，它不支持事务处理，也不能够容错**。如果你的硬盘崩溃了，那么数据文件就无法恢复了。如果你正在把`ISAM`用在关键任务应用程序里，那就必须经常备份你所有的实时数据，通过其复制特性，MYSQL能够支持这样的备份应用程序。

  #### MyISAM
  > `MyISAM`是MySQL的`ISAM`扩展格式和缺省的数据库引擎。**除了提供ISAM里所没有的索引和字段管理的大量功能，MyISAM还使用一种表格锁定的机制，来优化多个并发的读写操作，其代价是你需要经常运行OPTIMIZE TABLE命令，来恢复被更新机制所浪费的空间**。`MyISAM`还有一些有用的扩展，例如用来修复数据库文件的MyISAMCHK工具和用来恢复浪费空间的 MyISAMPACK工具。`MYISAM`强调了**快速读取操作**，这可能就是为什么MySQL受到了WEB开发如此青睐的主要原因：在WEB开发中你所进行的大量数据操作都是读取操作。所以，大多数虚拟主机提供商和INTERNET平台提供商只允许使用`MYISAM`格式。**MyISAM格式的一个重要缺陷就是不能在表损坏后恢复数据。**

  #### InnoDB
  > `InnoDB`数据库引擎都是造就MySQL灵活性的技术的直接产品，这项技术就是 *MYSQL+API*。在使用MYSQL的时候，你所面对的每一个挑战几乎都源于`ISAM`和`MyISAM`数据库引擎不支持事务处理（transaction process）也不支持外来键。尽管要比`ISAM`和`MyISAM`引擎慢很多，但是`InnoDB`包括了对**事务处理**和**外来键**的支持，这两点都是前两个引擎所没有的。如前所述，如果你的设计需要这些特性中的一者 或者两者，那你就要被迫使用后两个引擎中的一个了。

  #### HEAP（MEMORY）
  > `HEAP`允许**只驻留在内存里的临时表格**。驻留在内存里让`HEAP`要比`ISAM`和`MYISAM`都快，但是它所管理的数据是**不稳定**的，而且**如果在关机之前没有进行保存，那么所有的数据都会丢失**。在数据行被删除的时候，`HEAP`也不会浪费大量的空间。`HEAP`表格在你需要使用SELECT表达式来选择和操控数据的时候非常有用。要记住，在用完表格之后就删除表格。

  #### MyISAM与InnoDB的区别
  > 基本的差别为：`MyISAM`类型**不支持事务处理等高级处理，而InnoDB类型支持**。
  `MyISAM`类型的表强调的是*性能*，其执行数度比`InnoDB`类型更快，但是 *不提供事务支持* ，而`InnoDB` *提供事务支持* 以及 *外部键* 等高级数据库功能。

  #### 参考
  <https://www.cnblogs.com/zhangjinghe/p/7599988.html>
  <https://blog.csdn.net/t146lla128xx0x/article/details/78737290>

### CREATE TABLE

  #### AUTO_INCREMENT

  * `AUTO_INCREMENT` 必须设置为 `PRIMARY KEY`

  * 设置起始值 `AUTO_INCREMENT=100`

  #### CURRENT_TIMESTAMP

  * 在创建新记录的时候把这个字段设置为当前时间，但以后修改时，不再刷新它
  ``` SQL
  DEFAULT CURRENT_TIMESTAMP
  ```

  * 在创建新记录和修改现有记录的时候都对这个数据列刷新
  ``` SQL
  DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
  ```

  #### 参考
  <https://www.cnblogs.com/microcat/p/6600091.html>

### INSERT

  #### INSERT IGNORE 与 INSERT INTO 的区别

  > `INSERT IGNORE` 与 `INSERT INTO` 的区别就是 `INSERT IGNORE` 会忽略数据库中**已经存在**的数据，如果数据库没有数据，就插入新的数据，如果有数据的话就**跳过这条数据**。这样就可以保留数据库中已经存在数据，达到在间隙中插入数据的目的。