### mysql 语句

- 使用concat函数，拼接字符串。

```sql
    SELECT CONCAT('UPDATE m_wtg SET aaaaa=NOW(),uts=NOW() WHERE `ID_ENV` = ''',id_env,''';')
    FROM wtg
```
-  replace字符串替换
    
```sql
 UPDATE `person_auth` SET `site` = REPLACE (`site`,'GLWH','JYSN')WHERE site LIKE '%GLWH%';
```
