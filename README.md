![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 查询SQL Server是实体还是虚拟的
#### Find If SQL Server Is Physical Or Virtual
**发布-日期: 2015年03月06日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这是确定服务器是物理机还是虚拟机的快速方法。
此查询还将返回服务器上的服务器名称，机器类型，版本，内部版本号，版本号和CPU数量。请记住，如果服务器是虚拟的，那么CPU的类型将始终是理论上的，而不是实体的。
另外，我用了xp_cmdshell'systeminfo'来返回完整的操作系统信息，因此你可以仔细检查查询，必要时可以获取计算机的CPU“类型”。


## English
Here’s a quick way to determine if the server is a physical machine, or virtual machine.
This query will also return the Server Name, Machine Type, Edition, Build Number, Version Number, and Number of CPU’s on the server. Keep in mind if the server is Virtual then the type of CPU’s will always be logical, and not physical.
Additionally I’ve included the xp_cmdshell ‘systeminfo’ to return the full set of OS information so you can double check the query, and if necessary get the ‘type’ of CPU in the machine.


---
## Logic
```SQL
use master;
set nocount on
 
select
'Server Name' = serverproperty('computernamephysicalnetbios')
,   'Machine Type' = case sdosi.virtual_machine_type when '1' then 'Virtual Machine' when '0' then 'Physical Machine' end , 'Edition' = serverproperty('edition')
,   'Build' = serverproperty('productlevel')
,   'Version Number'    = serverproperty('productversion')
,   'CPU Count' = sdosi.cpu_count
from
sys.dm_os_sys_info sdosi;
 
exec xp_cmdshell 'systeminfo';


```

希望对你有用~ (Hope this is useful.)



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

