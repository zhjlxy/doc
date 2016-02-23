### linux 命令笔记
#### grep　匹配字符串，输出整行。
    grep -[acinv] '搜索内容串' filename 
    -a 以文本文件方式搜索 
    -c 计算找到的符合行的次数 
    -i 忽略大小写 
    -n 顺便输出行号 
    -v 反向选择，即找 没有搜索字符串的行 
    其中搜索串可以是正则表达式! 
示例：

    cat map_scada_log.log.3 map_scada_log.log.2 map_scada_log.log.1 | grep -i '^\[info\] 2016-01-15 10:[0-5][0-9]:[0-5][0-9]' | grep site_status |grep WF0003 | grep 'query finish' >site_status_WF003.log
    
    该条命令用户将map_scada_log.log.3、map_scada_log.log.2、map_scada_log.log.1 三个文件中2016-01-15日，10点到11点一个小时内，WF0003 的site_status 接口查询成功的日志写入site_status_wf003.log文件中