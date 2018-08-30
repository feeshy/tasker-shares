[中文](https://github.com/feeshy/tasker_profiles_share/blob/master/Wechat_Alerts/readme.md#%E5%BE%AE%E4%BF%A1%E7%9A%84%E9%AB%98%E7%BA%A7%E9%80%9A%E7%9F%A5)
|
[English](https://github.com/feeshy/tasker_profiles_share/blob/master/Wechat_Alerts/readme.md#advanced-notification-alerts-for-wechat)

# 微信的高级响铃控制

## 运行环境
`Android 5.0 以上的系统`, `Tasker`, `微信`

微信的通知已打开，铃声和震动已关闭。如果使用了其他的微信通知增强插件，铃声和震动也已关闭。

## 需求

微信“勿扰模式”下能响铃的bug存在了三年，看起来直到世界末日都没有修复的意思。

它自带的勿扰只能夜间按时段静音。如果我们给Android系统设置了“若连到某个Wifi或到达某个位置，则进入勿扰模式”之类的自动化配置。而这时微信依然能响，就很惹人烦，甚至很尴尬。

最近仔细想了想，用Tasker完全可以解决这个问题。思路就是把微信的通知和响铃一分为二，通知由微信自己完成（或者一些增强性的插件），响铃则交由Tasker来完成，顺便赋予微信堪比Telegram的自定义响铃特性。

美中不足的是，按好友/按群的自定义实现起来有些困难，这个自定义目前是对微信全局生效的。

## 配置说明

以下两种情况将不会响铃和计数

1. 屏幕打开时

2. 系统处于勿扰模式时

关屏、收到微信的通知之后，就会激活本profile：

* 前面`5`个通知正常响铃/震动；

* 当未读通知达到`5`个后，改为每`1`分钟最多响`1`次

  *这几个数字都可以根据自己的习惯调整*

* 微信前台运行时，计数自动归零。

  *如果只是消除通知，只要没打开微信界面，计数就不会清零。*

## 与酷安流行App的关系

这个Tasker Profile的目的是控制响铃和震动。
相比同类产品 [QTW通知助手](https://www.coolapk.com/apk/cn.vove7.qtmnotificationplugin)，这个Tasker配置不需要安装额外的App，且只需很简单的修改，就可以监听任一个其他App；但如果想实现对好友、群的自定义提醒，配置起来会比较麻烦。

而与微信、QQ的通知增强App，例如
[通知增强 for 微信](https://www.coolapk.com/apk/me.zhanghai.android.wechatnotificationtweaks2)、
[QQ消息扩展](https://www.coolapk.com/apk/com.inklin.qqnotfandshare)
并不形成竞品关系。
如果你对它们的响铃不满意，可以关掉它们的声音和震动。改用这个Tasker Profile监听它们，来替代它们响铃。

## XML 下载

https://raw.githubusercontent.com/feeshy/tasker_profiles_share/master/Wechat_Alert/wechat_alert.prf.xml

https://raw.githubusercontent.com/feeshy/tasker_profiles_share/master/Wechat_Alert/wechat_alert_clear.prf.xml

- - -
# Advanced notification alerts for Wechat

## Requirement

`Android 5.0+`, `Tasker`, `Wechat`

Wechat notification turned on and fully muted.

## Demand

Wechat for Android has not supported 'Do Not Disturb' mode for 3 years. Sometimes, I find it quite annoying.

My solution here is to fully mute the notification of Wechat, and let Tasker make sounds/vibs for it.

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
