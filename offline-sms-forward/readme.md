- import from github
	- https://github.com/feeshy/tasker-shares/raw/master/offline-sms-forward/SMS转发.prf.xml


# 适合双号双机的离线短信转发

```#短信转发``` ```#Tasker``` ```#双号双机``` ```#离线```

目前热门的短信推送方法有很多。例如：

支持跨平台推送的 [Pushbullet](https://www.pushbullet.com/)

可以微信推送的 [Server酱](https://sc.ftqq.com/)

它们的用户中，有一部分是在这样的情形下使用：

拥有两个电话号码、两部手机。平时只随身携带其中的一部，另一部则是低资费的套餐，一般放在包的深处（或其他不方便随时取用的地方），在需要查收验证码和其他短信时，如果不能自动把短信推送到主力机，就免不了一通翻找。

以上热门方法的共同特点是——基于网络。而保号套餐一般是不含套内流量的。在不开启移动数据的情况下，以上的方法就无效了。

这里尝试为这种情景提出一种不依赖网络的解决方案。（尤其适合每月赠送300条短信的联通保号用户。）

## 前提条件

1. Android备机：安装了 [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) ，已授予必要权限，并启用了本profile。

2. 主机可以正常收发短信。除此之外没有其他要求。

## 功能说明

1. 将备机收到的短信转发给主机。转发前会通过关键字的判断排除掉一些无用的营销信息。
	
		大diao 萌妹、激情 对射 更多，福利 加V信：uvw789246xyz 退订T
	
	触发关键字的不转发。

		我感冒了，好难受 ><
	
	未包含关键字的正常转发。

2. 备机进入等待状态，此时可以用主机回复备机进行如下操作：
		
		Re: 多喝热水
	
	用备机的号码向原发件人**回复**“多喝热水”。
	
		Fw:13800100500
	
	用备机的号码将刚才的短信**转发**13800100500。
	
		多喝热水，下班我就过去
	
	**无效**。回复任何非 ~~```Re:```~~ 、非 ~~```Fw:```~~ 开头的内容都会使备机退出等待状态。
 	
	“等待状态”只是一种方便理解的说法，实际上并不是一种持续的状态。无论退出与否，都不会影响性能与耗电。

3. 低排斥：如果你还有利用其他短信指令激活的profile（例如查询备机电量、位置等等），本profile与它们**不互斥**。

4. 单端配置：仅要求备机安装Tasker，而不依赖于主机上安装的任何软件。

	——主机的系统可以是iOS、Windows Phone、Sailfish……甚至功能机。
	
	如果两部都是Android手机，那么可以同时启用本profile，实现双向转发。在任一手机上都可以获得类似双卡手机的无缝体验。
	
## 思路

首先设计指令短信的格式

回复指令格式：
```^(?i)re:\s*[\s\S]*$```

re: + 任意个空格 + 回复的内容

转发指令格式：
```^(?i)fw:\s*(1[3-9][0-9])\d{8}$```

fw: + 任意个空格 + 13?~19?开头的11位手机号码

*当然，如果不想设定只能转发给手机的限制，也可以这样：*
*```^(?i)fw:\s*\d*$```*

-----

Tasker内置了两个可以直接使用的短信变量：短信正文 ```%SMSRB``` 、发件人 ```%SMSRF```。

但是这两个内置变量都是被最新的一条短信赋值的。当备机收到主机发送的指令之后，原内容就被指令短信覆盖了。

那么怎么实现回复/转发呢？

我的思路是，备机在做第一步的转发时，顺便定义两个中间变量：中间正文 ```%SMSSB```=```%SMSRB``` 、中间收件人 ```%SMSST```=```%SMSRF```。

当备机在第二步收到主机发来的回复指令时，只需要处理新的指令短信 ```%SMSRB```：首先删掉开头的指令 ```re:``` ，再把中间变量正文 ```%SMSSB``` 替换为指令短信余下的部分 ，而 ```%SMSST``` 保持不变。

同理接收到转发指令时，则是将中间收件人 ```%SMSST``` 替换为指令中的收件人，而中间正文 ```%SMSSB``` 不变。

这样无论回复还是转发，只要将正文变量 ```%SMSSB``` 发送给号码变量 ```%SMSST``` ，即达成目的。

-----

完整描述如下。配置时需要把其中的13800100500换成自己**另一台手机**的号码 ~~而**不是**本机号码~~

```
Profile: SMS转发
	Priority: 6 Enforce: no
	Event: Received Text [ Type:SMS Sender:* Content:* ]
Enter: SMS转发
	<SPAM>
	A1: If [ %SMSRF !~R ^\+?(86)?(1[3-9][0-9])\d{8}$ & %SMSRB ~R (退订|回复?)(TD?|N|QX|BK) |+ %SMSRB ~R (薇|威|V|W)(信|X) |+ %SMSRB ~R 福利|贷|信用卡|澳门|在家就能 ]
	A2: Stop [ With Error:Off Task: ] 
	<FORWARD>
	A3: Else If [ %SMSRF !~R 13800100500 ]
	A4: Send SMS [ Number:13800100500 Message:%SMSRB From: %SMSRF Store In Messaging App:Off ] 
	A5: Variable Set [ Name:%SMSST To:%SMSRF Recurse Variables:Off Do Maths:Off Append:Off ] 
	A6: Variable Set [ Name:%SMSSB To:%SMSRB Recurse Variables:Off Do Maths:Off Append:Off ] 
	<REMOTE COMMAND>
	A7: Else If [ %SMSRF ~R 13800100500 ]
	A8: If [ %SMSRB ~R ^(?i)re:\s*[\s\S]*$ ]
	A9: Variable Set [ Name:%SMSSB To:%SMSRB Recurse Variables:Off Do Maths:Off Append:Off ] 
	A10: Variable Search Replace [ Variable:%SMSSB Search:^re:\s* Ignore Case:On Multi-Line:Off One Match Only:Off Store Matches In: Replace Matches:On Replace With: ] 
	A11: Else If [ %SMSRB ~R ^(?i)fw:\s*(1[3-9][0-9])\d{8}$ ]
	A12: Variable Set [ Name:%SMSST To:%SMSRB Recurse Variables:Off Do Maths:Off Append:Off ] 
	A13: Variable Search Replace [ Variable:%SMSST Search:^fw:\s* Ignore Case:On Multi-Line:Off One Match Only:Off Store Matches In: Replace Matches:On Replace With: ] 
	A14: Else 
	A15: Goto [ Type:Action Label Number:1 Label:CLEAR ] 
	A16: End If 
	A17: Send SMS [ Number:%SMSST Message:%SMSSB Store In Messaging App:Off ] 
	<CLEAR>
	A18: Variable Clear [ Name:%SMSST Pattern Matching:Off Local Variables Only:Off ] 
	A19: Variable Clear [ Name:%SMSSB Pattern Matching:Off Local Variables Only:Off ] 
	A20: End If 
```
