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
 
