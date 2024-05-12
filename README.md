> [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm)是一个售价$3.49的Android自动化工具。提供丰富的接口和图形化的交互方式，无需学习代码即可编程解决问题。还可接入丰富的第三方插件进行跨应用交互。这个repository分享一些我个人常用的Tasker配置，希望这些自动化操作能使你的Android手机更加智能

- 发布地址
	- [Github](https://feeshy.github.io/tasker-shares/)[^github]
	- [TaskerNet](https://taskernet.com/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D)

[^github]: [github repo](https://github.com/feeshy/tasker-shares) 配置按目录存放，您可以按照每个目录中```readme.md```说明的思路自己创建，亦可直接下载```*.xml```文件导入。存放的其他类型的文件非必须。

## 目录

- [Aria2 离线下载](aria2/) - 将Android上的链接发送到VPS、NAS等远程设备上的Aria2进行离线下载
- [Bark推送](bark/#推送链接或文本) - 从通知栏磁贴、文本选择菜单、分享菜单等入口运行，把传入的或者是剪贴板中的链接、文本推送到[Bark App](https://apps.apple.com/cn/app/id1403753865)。
- [日租卡自动关数据](daily-metered-cellular/) - 在每月21日~月底的午夜自动关闭移动数据开关，防止不知不觉中开启下一天计费。可根据实际情况自行调整生效日期的范围
- [定时切换日/夜模式](night-mode/) - 定时切换夜间模式、免打扰、系统音量、同步、飞行模式（其中飞行模式切换需要root权限）
- 短信转发: 将一台Android手机所接收的短信转发至另一台手机
	- [用Bark或短信转发验证码](bark/#转发验证码)
	- [用Pushbullet或短信转发](pushbullet/#短信转发)
	- [仅用短信转发](offline-sms-forward/)
- [Pushbullet集成](pushbullet/)
	- [未接来电转发](pushbullet/#未接来电转发) - 使用Pushbullet或短信将Android手机的未接来电发送至另一台手机。
	- [远程短信](pushbullet/#远程短信) - Pushbullet提供用PC或者平板遥控安卓手机发短信的功能，但你无法用一台手机遥控另一台手机发短信。本profile尝试补齐此需求。
-  [抖音快手音量标准化](tiktok-normalizer/) - 刷抖音、快手时自动将媒体音量降低30%，退出时恢复原来的音量
 - [微信的高级响铃控制](wechat-alerts/) - 尝试修复微信Android版在勿扰模式下仍然能响铃的bug，并赋予其更高级的响铃控制。

## Links

- [Tasker Userguide](https://tasker.joaoapps.com/userguide_summary.html)
- Community
  - [Tasker Google Forum](https://groups.google.com/forum/#!forum/tasker) (official)
  - [Tasker Forum](https://forum.joaoapps.com/index.php?forums/tasker/) (official)
  - [r/Tasker](https://www.reddit.com/r/tasker/)
  - [Tasker中文交流群组](https://t.me/taskercn)
- Google Play
  - [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm)
  - Plugins:
    - [AutoInput](https://play.google.com/store/apps/details?id=com.joaomgcd.autoinput)
    - [AutoShare](https://play.google.com/store/apps/details?id=com.joaomgcd.autoshare)
    - [Secure Settings](https://play.google.com/store/apps/details?id=com.intangibleobject.securesettings.plugin)
    - [Pushbullet](https://play.google.com/store/apps/details?id=com.pushbullet.android)
