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
    
#### linux 去除重复的行
##### uniq干什么用的
    文本中的重复行，基本上不是我们所要的，所以就要去除掉。linux下有其他命令可以去除重复行，但是我觉得    uniq还是比较方便的一个。使用uniq的时候要注意以下二点
    1，对文本操作时，它一般会和sort命令进行组合使用，因为uniq 不会检查重复的行，除非它们是相邻的行。如果您想先对输入排序，使用sort -u。
    2，对文本操作时，若域中为先空字符(通常包括空格以及制表符)，然后非空字符，域中字符前的空字符将被跳过
    
##### 用法：uniq [选项]... [文件]、
  
    从输入文件或者标准输入中筛选相邻的匹配行并写入到输出文件或标准输出。    
    不附加任何选项时匹配行将在首次出现处被合并。        
    长选项必须使用的参数对于短选项时也是必需使用的。  
     -c, --count              //在每行前加上表示相应行目出现次数的前缀编号  
     -d, --repeated          //只输出重复的行  
     -D, --all-repeated      //只输出重复的行，不过有几行输出几行  
     -f, --skip-fields=N     //-f 忽略的段数，-f 1 忽略第一段  
     -i, --ignore-case       //不区分大小写  
     -s, --skip-chars=N      //根-f有点像，不过-s是忽略，后面多少个字符 -s 5就忽略后面5个字符  
     -u, --unique            //去除重复的后，全部显示出来，根mysql的distinct功能上有点像  
     -z, --zero-terminated   end lines with 0 byte, not newline  
     -w, --check-chars=N      //对每行第N 个字符以后的内容不作对照  
     --help              //显示此帮助信息并退出  
     --version              //显示版本信息并退出  
    