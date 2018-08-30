# 微信的高级通知
## 运行环境
`Android 5.0 以上的系统`, `Tasker`, `微信`

微信软件内的通知提醒已打开，并已静音+关闭震动

## 需求

微信“勿扰模式”下能响铃的bug存在了三年，看起来直到世界末日都没有修复的意思。

它自带的勿扰只能夜间按时段静音。如果我们给Android系统设置了若连到某个Wifi或到达某个位置，则进入“勿扰模式”的自动化功能。而时候微信依然能响，就很惹人烦，甚至很尴尬。

仔细想了想，用Tasker完全可以解决这个问题。思路就是把微信的通知和响铃一分为二，通知由微信自己完成（或者一些增强性的插件），响铃则交由Tasker来完成，顺便赋予微信堪比Telegram的自定义响铃特性。

美中不足的是，按好友/按群的自定义实现起来有些困难，这个自定义目前是对微信全局生效的。

## 配置说明


## XML 下载

https://raw.githubusercontent.com/feeshy/tasker_profiles_share/master/Wechat_Alert/wechat_alert.prf.xml

https://raw.githubusercontent.com/feeshy/tasker_profiles_share/master/Wechat_Alert/wechat_alert_clear.prf.xml

- - -
# Advanced notification alerts for Wechat

## Requirement

`Android 5.0+`, `Tasker`, `Wechat`

Wechat notification turned on and fully muted.

## Demand

Wechat for Android has not supported 'Do Not Disturb' mode for 3 years. Sometimes, it can be quite annoying.

My solution here is to fully mute the Wechat app, and let Tasker alert for it.

And inspired from Telegram, I add some custom options for this profile, which might be useful for group chats.

## Instructions

This profile will not be triggered on the follwing occasions:

1. When display on

2. When Android 'Do Not Disturb' mode turned on (either priority, alarm, or none)

Beyond these two cases, when your device receives notifications from wechat, Tasker will act as following:

* For the first `5` notifications, your device will alert just as usual.

* Once unread counts reaches the limit `5`, your device will get no more than `1` alerts every `1` minute.

  *These values are all adjustable*

* Once you open Wechat, the unread counts is reset to 0.

  *Dismissing notifications will not reset.*

## XML Download

https://raw.githubusercontent.com/feeshy/tasker_profiles_share/master/Wechat_Alert/wechat_alert.prf.xml

https://raw.githubusercontent.com/feeshy/tasker_profiles_share/master/Wechat_Alert/wechat_alert_clear.prf.xml
