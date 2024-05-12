- import from github
	- https://github.com/feeshy/tasker-shares/raw/master/tiktok-normalizer/tiktok-normalizer.prf.xml
- import from taskernet
	- https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3A%E6%8A%96%E9%9F%B3%E5%BF%AB%E6%89%8B%E9%9F%B3%E9%87%8F%E6%A0%87%E5%87%86%E5%8C%96

# 抖音快手音量标准化

保护你的耳朵和音量键。打开抖音、快手时自动将媒体音量降低30%，退出时恢复

![](Screenshot_20210713-102207.jpg)

```
Profile: 抖音快手音量标准化
	Application: 抖音, 抖音火山版, 抖音极速版...
Enter: 保护耳朵
	A1: Variable Set [ Name:%volTiktok To:round ( %VOLM * 0.7 ) Recurse Variables:Off Do Maths:On Append:Off Max Rounding Digits:3 Structure Output (JSON, etc):On ] 
	A2: Flash [ Text:音量已由 %VOLM 降低至 %volTiktok Long:Off ] 
	A3: Media Volume [ Level:%volTiktok Display:Off Sound:Off ] 
```