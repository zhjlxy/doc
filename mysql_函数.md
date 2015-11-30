### mysql 语句

1、使用concat函数，拼接字符串。

    SELECT CONCAT('UPDATE m_wtg SET aaaaa=NOW(),uts=NOW() WHERE `ID_ENV` = ''',id_env,''';')
    FROM wtg 