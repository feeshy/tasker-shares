- import from taskernet
	- https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3A%E8%87%AA%E5%8A%A8%E5%85%B3%E6%95%B0%E6%8D%AE

# 日租卡自动关数据

在每天午夜关闭移动数据开关，防止不知不觉中开启下一天计费

默认每月21日~月底生效，建议根据实际情况自行调整日期范围

[点我导入](https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3A%E8%87%AA%E5%8A%A8%E5%85%B3%E6%95%B0%E6%8D%AE)，或者按照下面的描述从零创建

```
Profile: 自动关数据
	Cooldown: 43200 Priority: 10 Restore: no
	Time: From 23:58 Till 00:01
	Day: The 21st, 22nd, 23rd, 24th, 25th, 26th, 27th, 28th, 29th, 30th, 31st or Last
Enter: 自动关数据
	A1: WiFi Tether [ Set:Off Keep Wi-Fi when turning on:Off ] If [ %TETHER ~ wifi ]
	A2: Mobile Data [ Set:Off ] 
```