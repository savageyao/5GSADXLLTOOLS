5G SA 定向流量脚本生成工具（ZTE）

一、	运行环境

Python3.9
需额外安装netaddr和openpyxl模块。其中netaddr模块用于IP地址处理（判断IP异常，IPv4/IPv6，地址重复），openpyxl模块用于excel文件读取。（建议IDE使用PyCharm）

二、	运行方法

1.	抓取UPF上的现网规则
从UPF上分别抓取SHOW L34FILTER; SHOW L34FILTERGROUP两条命令的输出结果，将CSV文件放到Python程序目录下，确保程序目录下存在“rules”文件夹
2.	检查集团下发的定向流量规则表格
确认集团表格为xlsx格式，将excel文件放到Python程序相同目录下。
3.	修改入参后运行
修改程序中的入参文件改为集团下发的定向流量规则文件名。认为集团提供的是全量数据，对旧规则有而集团无的L34规则不删除。
4.	运行程序
会检测UPF存量规则是否存在重复，不输出去重脚本。在rules目录会输出配置脚本。

三、	建议事项

1.	规则和规则组规范写法

  l34filername:l34_f_{RG}_{YYYYMMDD}_{NUM}

  l7filername:l7_f_{RG}_{YYYYMMDD}_{NUM}

  l34filtergrp:l34_g_{RG}_1

  l7filtergrp:l7_g_{RG}_1

  RG：9-10位长度的整数

  YYYYMMDD: 8位长度年月日

  NUM：三位长度整数，不足三位前补0


四、	注意事项

仅适用于中兴核心网设备
仅适用于存量RG规则的更新。如新增RG，需要额外配置。
