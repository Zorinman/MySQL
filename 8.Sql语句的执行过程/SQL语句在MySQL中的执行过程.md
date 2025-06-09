[javeguild的解释](https://javaguide.cn/database/mysql/how-sql-executed-in-mysql.html) 
注意最后总结更新语句的执行流程是错误的❌的“`更新语句执行流程如下：分析器---->权限校验---->执行器--->引擎---redo log(prepare 状态)--->binlog--->redo log(commit 状态)`” 


正确的应该是和查询一样的流程，只是后面调用存储引擎之后存储引擎的操作更加复杂

具体看[一条Update语句的执行过程是怎样的](https://zhuanlan.zhihu.com/p/639174065)





