### mysql 语句

- 使用concat函数，拼接字符串。

```sql
    SELECT CONCAT('UPDATE m_wtg SET aaaaa=NOW(),uts=NOW() WHERE `ID_ENV` = ''',id_env,''';')
    FROM wtg
```
```sql
SELECT CONCAT("UPDATE `m_site` SET id='",t3.id,"' WHERE  ALIAS_SCD = '",t3.alias_scd,"';") FROM 
(
SELECT * FROM `m_site` t2 WHERE 
t2.`ENERGY_TYPE` ='solar' AND  t2.`ID` != t2.`ALIAS_SCD`
AND t2.`ALIAS_SCD` IN(SELECT t1.`ALIAS_SCD` FROM `m_site` t1 WHERE t1.`ENERGY_TYPE` ='solar' AND  t1.`ID` = t1.`ALIAS_SCD`)
) t3;
```
-  replace字符串替换
    
```sql
 UPDATE `person_auth` SET `site` = REPLACE (`site`,'GLWH','JYSN')WHERE site LIKE '%GLWH%';
```
 
- SQL合并查询结果
    - UNION的作用
 UNION 指令的目的是将两个 SQL 语句的结果合并起来。从这个角度来看， UNION 跟 JOIN 有些许类似，因为这两个指令都可以由多个表格中撷取资料。 UNION 的一个限制是两个 SQL 语句所产生的栏位需要是同样的资料种类。另外，当我们用 UNION这个指令时，我们只会看到不同的资料值 (类似 SELECT DISTINCT)。 union只是将两个结果联结起来一起显示，并不是联结两个表。
 2. Union All
UNION ALL 这个指令的目的也是要将两个 SQL 语句的结果合并在一起。 UNION ALL 和 UNION 不同之处在于 UNION ALL 会将每一笔符合条件的资料都列出来，无论资料值有无重复。

```sql
SELECT 
  t3.`ADDRESS`,
  t1.`ID`,
  t1.`NAME_CHN` 
FROM
  `m_site` t1,
  `engine` t2,
  `scada_address` t3 
WHERE t3.`ADDRESS_ID` = t2.`ADDRESS_ID` 
  AND t1.`ID` = t2.`SITE_ID` 
  AND t1.`STATE` = 'Y' 
  AND t1.`ALIAS_SCD` != '' 
UNION
ALL 
SELECT 
  (SELECT 
    ADDRESS 
  FROM
    `scada_address` 
  WHERE address_id = '1') AS ADDRESS,
  t11.`ID`,
  t11.`NAME_CHN` 
FROM
  `m_site` t11 
WHERE t11.`STATE` = 'Y' 
  AND t11.`ALIAS_SCD` != '' 
  AND t11.`ID` NOT IN 
  (SELECT 
    t1.`ID` 
  FROM
    `m_site` t1,
    `engine` t2,
    `scada_address` t3 
  WHERE t3.`ADDRESS_ID` = t2.`ADDRESS_ID` 
    AND t1.`ID` = t2.`SITE_ID` 
    AND t1.`STATE` = 'Y' 
    AND t1.`ALIAS_SCD` != '' 
  ORDER BY t3.`ADDRESS`) 
ORDER BY ADDRESS ;
``` 


- group_concat

        函数作用： 当SQL语句中使用到....group by....的时候， 该函数能够将相同的行组合起来。
        select * from goods;  

        +------+------+
        | id| price|
        +------+------+
        |1 | 10|
        |1 | 20|
        |1 | 20|
        |2 | 20|
        |3 | 200 |
        |3 | 500 |
        +------+------+
        
        以id分组，把price字段的值在同一行打印出来，逗号分隔(默认)

        select id, group_concat(price) from goods group by id;  
        
        +------+--------------------+
        | id| group_concat(price) |
        +------+--------------------+
        |1 | 10,20,20|
        |2 | 20 |
        |3 | 200,500|
        +------+--------------------+
        
        以id分组，把price字段的值在一行打印出来，分号分隔 
        select id,group_concat(price separator ';') from goods group by id;  
        +------+----------------------------------+
        | id| group_concat(price separator ';') |
        +------+----------------------------------+
        |1 | 10;20;20 |
        |2 | 20|
        |3 | 200;500 |
        +------+----------------------------------+
        
        以id分组，把去除重复冗余的price字段的值打印在一行，逗号分隔
        select id,group_concat(distinct price) from goods group by id;  
        +------+-----------------------------+
        | id| group_concat(distinct price) |
        +------+-----------------------------+
        |1 | 10,20|
        |2 | 20 |
        |3 | 200,500 |
        
        以id分组，把price字段的值打印在一行，逗号分隔，按照price倒序排列
        select id,group_concat(price order by price desc) from goods group by id;  
        +------+---------------------------------------+
        | id| group_concat(price order by price desc) |
        +------+---------------------------------------+
        |1 | 20,20,10 |
        |2 | 20|
        |3 | 500,200|