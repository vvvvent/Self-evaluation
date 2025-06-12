# Self-evaluation

42233099 曾慧鑫 数据科学与大数据技术

## 1.知识积累（16/20）

### 第一周：软件下载
学习内容：
- 简单了解数据库；
- 下载DataGrip、Postgres；
- 创建数据库mydb。
成果：
- 成功地下载DataGrip、Postgres；
photo
- 创建了数据库mydb，因为环境配置问题在DataGrip连接不到数据库。（该问题在第五周实验课求助助教和老师帮忙解决了。）
### 第二周：深入了解数据库
学习内容：
- 什么是数据库；
- 数据库的应用；
- 数据库的在应用中优点；
- 数据库语言、数据视图。
成果：
- 明确数据库是按照数据结构来组织、存储和管理数据的仓库，掌握其结构化、集成化、共享性等核心特征，能区分数据库与普通文件存储的差异。
- 熟悉数据库在金融交易记录、电商商品管理、医疗病历存储、社交平台用户数据管理等场景的应用，理解其在不同行业的适配性与重要性。
- 认识到数据库可有效减少数据冗余、保障数据一致性与完整性、实现多用户共享访问、通过权限控制提升数据安全性，以及利用索引等技术优化数据查询效率。
- 掌握 SQL 语言进行数据定义（DDL）、数据操纵（DML）、数据控制（DCL）的基本操作；理解外模式、模式、内模式三层数据视图的作用，以及视图如何实现数据的逻辑独立性与安全性。
### 第三周：关系模型
学习内容：
- 关系数据库；
- 码（主码、超码、候选码、外码）；
- 关系代数。
成果：
- 以二维表组织数据，具结构化、共享性等特性，区别于非关系型数据库。
- 主码唯一标识元组，候选码是主码备选，超码包含候选码，外码用于表间关联；学会建立表，标注主码。
```
  CREATE TABLE instructure (
    ID INT PRIMARY KEY,
    name VARCHAR(50),
    dept_name VARCHAR(50),
    salary DECIMAL(10, 2),
);
```
- 掌握选择、投影、连接等基本运算，用于数据查询与处理。
### 第四周
学习内容：
- 基本类型（字符、数）；
- 定义关系（creat table）；
- 查询关系（select）；
- 更名运算、排序子句。
成果：
- 掌握字符型、数值型等基础数据类型，明确其存储格式与适用场景。
```  
int：整数类型；

smallint：小整数整形；

numeric(p, d)：定点数，有p为数字，小数点右边有d位；

float(n)：精度至少为n位的浮点数；

real, double precision：浮点数与双精度浮点数。
```
- 熟练使用CREATE TABLE语句定义表结构，包括字段名、数据类型，实现数据结构化存储。
- 运用SELECT语句完成单表数据查询。
```
select name from instructor;
select distinct dept_name from instructor;
```
在查询的时候经常忘记要去除重复！
- 利用排序子句（ORDER BY）按指定规则对查询结果排序。
```
select *
from instructor
order by salary desc, name asc;
```
desc是降序；asc是升序。
### 第五周：环境搭建（实验课）
学习内容：
- 连接数据库，执行 SQL 文件；
- 字符串相关操作；
- 集合操作。
成果：
- 由于对MacOS系统的不熟悉，导致花费了大量的时间在连接数据库上，好在最后解决了。
photo
- 使用SQL字符串函数（CONCAT、SUBSTRING）处理文本数据，实现模糊查询、格式转换。
- 运用UNION、INTERSECT、MINUS（并、交、差）集合操作符合并或筛选多表查询结果，保证数据一致性与完整性。
### 第六周：空值和聚合查询
学习内容：
- null值的处理；
- 聚集函数、分组聚集；
- in, not in, > some, > al。
成果：
- 掌握IS NULL/IS NOT NULL判断空值，能用COALESCE/NULLIF函数处理空值场景。
```
SELECT * FROM instructor
WHERE (salary > 80000) IS UNKNOWN;
SELECT * FROM instructor
WHERE (salary > 80000) IS NOT UNKNOWN;
```
SQL还支持使用is unknown对布尔结果进行测试：
- 使用COUNT/SUM/AVG等聚集函数，结合GROUP BY实现分组统计，配合HAVING过滤分组结果。
```
SELECT dept_name, count (DISTINCT instructor.id)
FROM instructor, teaches
WHERE instructor.id = teaches.id
AND semester = 'Spring'
AND year = 2018
GROUP BY dept_name; 24
```
在很多场景下，GROUP BY的查询是不合法的。
- 用IN/NOT IN匹配集合元素，通过> SOME（大于任一）、> ALL（大于所有）实现多值条件筛选。
### 第七周：修改数据库
学习内容：
- 增、删、改；
- DDL（修改关系）；
- SQL排名。
成果：
- 用INSERT、DELETE、UPDATE语句进行数据增删改，准确控制数据变化范围。
- 掌握DDL语句（如ALTER TABLE），可修改表结构、添加或删除列、调整约束条件，适应业务需求变更。
```
ALTER TABLE products ADD COLUMN description text;
```
新增属性
- 运用RANK()、DENSE_RANK()、ROW_NUMBER()等窗口函数实现数据排名，支持按特定字段进行升降序排名展示。
```
SELECT id, salary FROM instructor
ORDER BY salary DESC;
```
按照工资的降序进行排序
### 第八周：中级 SQL
学习内容：
- 连接；
- 完整性约束；
- 数据视图。
成果：
- 掌握连接类型和连接条件
```
连接类型 (join types)：
• inner join
• left outer join
• right outer join
• full outer join
连接条件 (join conditions)：
• natural join
• on <predicate>
• using (A1, A2, ..., An)
```
- 使用内连接、外连接、交叉连接等操作，实现多表数据关联查询，获取复杂业务场景所需的整合数据。
##### 默认join是inner有left/right/full，肯定是outernatural join是连接的条件，而不是类型
- 掌握实体完整性、参照完整性和用户定义完整性的约束方法，通过主键、外键、CHECK 等语句保障数据准确性与一致性。
- 学会创建和使用数据视图，实现数据的逻辑独立性，简化复杂查询，并通过视图权限控制增强数据安全性。
### 第九周:高级 SQL（1）
学习内容：
- 高级数据类型（时间和日期）；
- 类型转换；
- 授权。
成果：
- 使用时间和日期类型（如DATE、TIME、TIMESTAMP）存储与处理时间序列数据，掌握日期函数实现数据筛选与计算。
```
SELECT current_date, current_time, current_timestamp;
SELECT current_time at time zone 'CCT';
SELECT current_time at time zone 'Asia/Shanghai';
SELECT CAST('2008-08-08' AS date);
SELECT date '2008/08/08';
```
实用的时间相关函数
- 通过显式（CAST、CONVERT）和隐式类型转换处理不同数据类型间的兼容性问题。
- 运用GRANT、REVOKE语句实现用户权限的精准分配与回收，保障数据库操作的安全性与合规性。
```
GRANT SELECT
ON department
TO lilei;
```
##### GRANT < 权限列表 >; ON < 关系或视图名 > ;TO < 用户或角色 >。

### 第十周：高级 SQL（2）
学习内容：
- 函数与过程；
- 动态SQL；
- SQL注入。
成果：
- 掌握自定义函数和存储过程的编写，实现复杂业务逻辑封装与复用。
```
CREATE FUNCTION calculate_discount(price DECIMAL) 
RETURNS DECIMAL AS $$
BEGIN
    RETURN price * 0.9;
END;
$$ LANGUAGE plpgsql;
```
创建了一个简单函数
- 学会使用动态 SQL 拼接执行语句，灵活应对参数可变的查询需求。
- 理解了SQL注入原理，掌握预编译语句、参数化查询等防护手段。
##### 使用简单的字符串拼接构造的SQL语句有SQL注入的风险！可以使用ORM或PreparedStatement避免这个问题

### 第十一周:ER 模型
学习内容：
- E-R 模型；
- 将E-R图转化成关系模式；
- E-R 模型的替代品（如UML图）。
成果：
- 运用E-R模型分析实体、属性及联系，能通过矩形、菱形、椭圆等图形符号准确表达数据结构与业务逻辑。
学生-考试（Student–Exam）多对多关系转换为关系表：
```
CREATE TABLE Student_Exams (
    student_id INT,
    exam_id INT,
    PRIMARY KEY (student_id, exam_id),
    FOREIGN KEY (student_id) REFERENCES Students(ID),
    FOREIGN KEY (exam_id) REFERENCES Exams(ID)
);
```
- 掌握将E-R图转化为关系模式的规则，包括实体集、联系集的表结构设计，以及主码、外码的确定。
根据题目要求做的ER图：
photo
- 了解UML图等替代工具的特点，对比其与E-R模型在数据库设计中的适用场景。
### 第十二周:关系数据库范式
学习内容：
- 模式分解；
- 函数依赖；
- BCNF, 3NF。
成果：
- 掌握模式分解的无损连接和保持函数依赖原则，能将复杂关系模式拆解为多个子模式，优化数据库结构。
- 识别数据间的函数依赖关系（如完全依赖、部分依赖、传递依赖），为模式设计与优化提供理论依据。
- 熟练运用3NF和BCNF范式规则，消除数据冗余与更新异常，确保关系模式满足规范化要求。
3NF的定义
```
具有函数依赖集F的关系模式R属于3NF的条件是，对F中
所有形如α → β的函数依赖，下面至少一个成立：
• α→ β是平凡的函数依赖
• α是 R的一个超码
• β− α的每个属性都属于R的某个候选码
```
### 第十三周:存储、索引、查询及事务（上）
学习内容：
- 存储；
- 索引；
- 事务。
成果：
- 掌握数据库存储结构（如数据页、段表空间），了解数据物理存储与逻辑结构的映射关系，优化存储效率。
不同的存储模型：
```
INSERT INTO instructor(ID, name, salary, dept_name)
VALUES('5566', 'Mike', 60000, 'Music');

SELECT * FROM instructor
WHERE ID = '5566';

SELECT COUNT(*)
FROM instructor
WHERE department = 'Music';
```
- 熟悉B+树、哈希等索引类型，能根据查询需求创建合适索引，通过执行计划分析索引命中情况提升查询性能。
##### 哈希索引只支持等值操作符（=），不支持范围查询。
使用哈希索引时，数据库只能高效地查找精确匹配的值，如：
```
SELECT * FROM Students WHERE ID = 1001;
```
但对于范围查询，如：
```
SELECT * FROM Students WHERE ID > 1000;
```
哈希索引无法发挥作用，效率很低，甚至可能退化为全表扫描。

### 第十四周:存储、索引、查询及事务（下）
学习内容：
- 事务：指的是一组构成一个单一逻辑工作单元的操作集合。
成果：
- 理解ACID特性，掌握事务开启、提交、回滚操作，处理并发事务中的脏读、幻读等问题，保障数据一致性。
事务具有以下四个关键特性，通常称为ACID原则：
````
原子性（Atomicity）： 事务中的所有操作要么全部完成，要么全部不执行，不会出现部分完成的情况。

一致性（Consistency）： 事务执行前后，数据库必须保持一致的状态，满足所有定义的约束条件。

隔离性（Isolation）： 并发执行的多个事务之间应相互隔离，一个事务的中间状态对其他事务不可见。

持久性（Durability）： 一旦事务提交，其结果应永久保存，即使系统发生故障也不会丢失。
```
## 2.作业与随堂测试（20/20）
  
### 本学期课程共布置八次课后作业，我均严格遵循作业要求与提交时间节点，在规定期限内完成并准时提交。每次作业从资料查阅、思路梳理到内容撰写、格式调整，均经过系统规划与细致执行，确保作业完成质量，在这一部分我给了自己满分。
  
- homework01（https://github.com/vvvvent/Self-evaluation/blob/main/homework01.pdf）

- homework02（https://github.com/vvvvent/Self-evaluation/blob/main/homework02.pdf）

- homework03（https://github.com/vvvvent/Self-evaluation/blob/main/homework03.pdf）

- homework04（https://github.com/vvvvent/Self-evaluation/blob/main/homework04.pdf）

- homework05（https://github.com/vvvvent/Self-evaluation/blob/main/homework05.pdf）

- homework06（https://github.com/vvvvent/Self-evaluation/blob/main/homework06.pdf）

- homework07（https://github.com/vvvvent/Self-evaluation/blob/main/homework07.pdf）

- homework08（https://github.com/vvvvent/Self-evaluation/blob/main/homework08.pdf）

### 以下是完成作业时参考的书籍：

#### （1）《Database System Concepts》（第7版）- Abraham Silberschatz等  
该书系统地讲解许多数据库核心知识，如关系代数的数学定义、BCNF范式，为我完成课后作业提供了理论支撑。

#### （2）《SQL for Data Scientists: A Beginner's Guide》- Renee M. P. Teate  
作为数据分析导向的SQL实战手册，书中零售场景案例与课程项目中老师讲解过的在线零售数据库高度适配。特别是第4章关于嵌套查询优化的讲解，帮助我理解了子查询重构为JOIN操作。

#### （3）《NoSQL for Mere Mortals》- Dan Sullivan  
该书主要介绍非关系型数据库技术，对MongoDB、键值存储的原理阐释，结合homework07中MongoDB Compass实操经验，我深入理解了文档型数据库的灵活架构，通过书中第4章的CRUD操作指南，成功在本地环境完成JSON数据的高效存取。

## 3.与授课老师、同学与AI的互动（8/10）

### AI给予我的帮助：
在《数据库原理与应用》这门课上，AI俨然成为了我的第二老师。当我一些SQL语句知识点上卡顿时，AI总能通过结构化查询示例补充底层逻辑——尽管它的讲解不如老师的案例生动，但能以无限次提问的方式，帮我拆解问题。不止这门课程，在很多门课程上，AI都给予了我很多帮助，解决很多我一时难以解决的问题，教会我使用很多工具。AI带来的便捷性也助长我的惰性，在这门课程上有的时候我太过于依赖AI缺少了与同学和老师的互动。
### 与同学的相处：
在《数据库原理与应用》的学习过程中，与同专业好友的探讨成为我突破知识瓶颈的重要助力。面对错综复杂的索引体系，我时常陷入B+树索引、哈希索引与全文索引的概念迷宫，混淆聚簇索引与非聚簇索引的物理存储差异，或是在复合索引的最左匹配原则上屡屡犯错。每当我在习题练习或是在课堂提问环节迷茫时，她们帮我直观理解索引结构。这些知识共享的时刻，不仅填补了我的认知盲区，更让我在协作学习中深刻体会到数据库原理从理论到实践的转化逻辑。 
### 老师给予我的课堂体验：
陈老师带给我们的课堂风格是轻松愉悦的，师生互动频繁，虽然偶尔突如其来的提问会让我紧张得心跳加速，但这种提问式互动让我能够快速掌握知识点。在讲解关系代数时，老师以选课系统为例，将连接、投影等抽象操作具象化为学生与课程的关联查询；在介绍数据库设计时，又用物品零售场景模拟商品库存与销售记录的范式优化，这些贴近生活的案例，让晦涩的理论知识变得通俗易懂。每次收集到同学们关于课程节奏、案例类型的建议，他都会逐条认真研读，及时调整教学内容。
## 4.自我评价（44/50）

### 总分为三部分之和：16+20+6=44。每一部分的总分按照自己在这门课程中所花费的精力大致占比设置的。
