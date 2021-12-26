#5G SA定向流量配置辅助工具   
适用于中兴5G SA核心网设备UPF网元  
适用于存量RG规则的**增量/全量**更新   
如新增RG，需要额外增加配置
##运行环境
Python3.X  
netaddr >= 0.7.19  
openpyxl >= 3.0.0  

##场景
增量更新某个RG的定向流量规则。  
>upfdxllloose.py  

全量更新某个RG的定向流量规则。  
>upfdxllstrict.py   

##运行方法  

###1.抓取UPF上的现网规则  
>从每台UPF上分别抓取SHOW L34FILTER//L34FILTERGROUP/L7FILTER/L7FILTERGROUP四条命令的输出结果   
将输出的CSV文件放到Python程序目录下的cur目录  
按照upfXXX格式命名 
4个规则文件放在对应UPF目录下

###2.检查定向流量规则表格  

>确认xlsx格式的表格放到Python程序相同目录下  

###3.检查输出目录
a)	增量更新场景
确保程序目录下存在“rules”文件夹
 
b)	全量更新场景
确保程序目录下存在“allrules”文件夹
 
###4. 修改入参后运行  
修改对应行的定向流量规则文件名    
增量对旧规则有而表格无的L34/L7规则不删除   
增量不会/会检测L34/L7规则是否存在重复 **flag_chk_dupl**  
增量/存量在对应输出目录输出对应UPF配置脚本

##建议事项  

###1.规则和规则组写法  

|规则名|写法|
|:----:|:----:|
|l34filername|l34\_f\_\{RG\}\_\{YYYYMMDD\}\_\{NUM\}|
|l7filername|l7\_f\_\{RG\}\_\{YYYYMMDD\}\_\{NUM\}|
|l34filtergrp|l34\_g\_\{RG\}\_1| 
|l7filtergrp|l7\_g\_\{RG\}\_1|   

###2.RG：9-10位长度的整数  
###3.YYYYMMDD: 8位长度年月日  
###4.NUM：四位长度整数，不足四位前补0  

##注意事项

现网UPF规则差异较大建议全量更新(慎重)


