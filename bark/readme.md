[^1]: import from [taskernet](https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Task%3ABark)
[^2]: import from [taskernet](https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3APush+Text+to+Bark)
[^3]: import from [taskernet](https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3AShare+to+Bark)
[^4]: import from [taskernet](https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3A%E9%AA%8C%E8%AF%81%E7%A0%81%E8%BD%AC%E5%8F%91)

[Bark](https://github.com/Finb/Bark)是一个简约好用的，尤以iOS端无需进入App即可复制到剪贴板为特点的推送App。

## 预先准备

### 安装接收端

iOS：[Bark](https://apps.apple.com/cn/app/id1403753865) | Android：[Push Lite](https://github.com/xlvecle/PushLite/releases)

### 获取Push URL

安装Bark后，在App的主界面，可以看到形如 ```https://api.day.app/xxxxxxxxxx/``` 的Push URL，记录下来

![](https://wx3.sinaimg.cn/mw690/0060lm7Tly1g0bu1cv28lj30om0j6gng.jpg)

### 安装推送端

以下所有任务均依赖于[Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) ($3.49) 实现

其中的两个还需额外安装[AutoShare](https://play.google.com/store/apps/details?id=com.joaomgcd.autoshare)插件 ($1.49)

---

## 推送链接或文本

下面的任务可以从通知栏磁贴、文本选择菜单、分享菜单等等入口运行，帮你把剪贴板中的或者是传入的内容推送到Bark

> [参与讨论或反馈](https://meta.appinn.net/t/19189)

导入后记得把```https://api.day.app/xxxxxxxxxxxx/```修改成自己的Bark Push URL

### 通知栏磁贴或者桌面图标

导入任务[^1]或者按照下方的描述手动创建一个Tasker任务


```
Enter: Bark
	A1: Status Bar [ Set:Collapsed ] 
	A2: Variable Set [ Name:%clipboard To:%CLIP Recurse Variables:Off Do Maths:Off Append:Off Max Rounding Digits:3 ] 
	A3: Variable Search Replace [ Variable:%clipboard Search:(http(s)?:\/\/)?[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(\.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+(:[0-9]{1,5})?[-a-zA-Z0-9()@:%_\\\+\.~#?&//=]* Ignore Case:Off Multi-Line:Off One Match Only:On Store Matches In Array:%url Replace Matches:Off Replace With: Continue Task After Error:On ] 
	A4: If [ %url1 Set ]
	A5: HTTP Request [  Method:HEAD URL:https://api.day.app/xxxxxxxxxxxxxxxxxxxxxxxxxx/%e4%bb%8eAndroid%e7%bb%a7%e7%bb%ad?url=%url1 Headers: Query Parameters: Body: File To Send: File/Directory To Save With Output: Timeout (Seconds):10 Trust Any Certificate:Off Automatically Follow Redirects:Off Use Cookies:Off ] 
	A6: Else 
	A7: HTTP Request [  Method:HEAD URL:https://api.day.app/xxxxxxxxxxxxxxxxxxxxxxxxxx/%CLIP?automaticallyCopy=1 Headers: Query Parameters: Body: File To Send: File/Directory To Save With Output: Timeout (Seconds):10 Trust Any Certificate:Off Automatically Follow Redirects:Off Use Cookies:Off ] 
	A8: End If 
	A9: Flash [ Text:Pushed to Bark Long:Off ]  If [ %http_response_code ~ 200 ]
```

### 文本选择菜单

安装[AutoShare](https://play.google.com/store/apps/details?id=com.joaomgcd.autoshare)；然后导入Profile[^2]，或者按照下方的描述手动创建一个Profile

```
Profile: Push Text to Bark
	Restore: no
	Event: AutoShare Process Text [ Configuration:Text Processor: Tasker ]
Enter: Push to Bark
	A1: Variable Search Replace [ Variable:%astext Search:(http(s)?:\/\/)?[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(\.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+(:[0-9]{1,5})?[-a-zA-Z0-9()@:%_\\\+\.~#?&//=]* Ignore Case:Off Multi-Line:Off One Match Only:On Store Matches In Array:%url Replace Matches:Off Replace With: Continue Task After Error:On ] 
	A2: If [ %url1 Set ]
	<修改成自己的Push URL>
	A3: HTTP Request [  Method:HEAD URL:https://api.day.app/xxxxxxxxxxxx/%e4%bb%8eAndroid%e7%bb%a7%e7%bb%ad?url=%url1 Headers: Query Parameters: Body: File To Send: File/Directory To Save With Output: Timeout (Seconds):10 Trust Any Certificate:Off Automatically Follow Redirects:Off Use Cookies:Off Continue Task After Error:On ] 
	A4: Else 
	<修改成自己的Push URL>
	A5: HTTP Request [  Method:HEAD URL:https://api.day.app/xxxxxxxxxxxx/%astext?automaticallyCopy=1 Headers: Query Parameters: Body: File To Send: File/Directory To Save With Output: Timeout (Seconds):10 Trust Any Certificate:Off Automatically Follow Redirects:Off Use Cookies:Off Continue Task After Error:On ] 
	A6: End If 
	A7: If [ %http_response_code ~ 200 ]
	A8: Flash [ Text:Pushed to Bark Long:Off ] 
	A9: Else 
	A10: Flash [ Text:Failed to Push Long:Off ] 
	A11: End If 
```

### 分享菜单

安装[AutoShare](https://play.google.com/store/apps/details?id=com.joaomgcd.autoshare)；然后导入Profile[^3]，或者按照下方的描述手动创建一个Profile

```
    Profile: Share to Bark (21)
    	Restore: no
    	Event: AutoShare [ Configuration:Command: all
    Sender: all
    Subject: all
    Text: all
    File: all ]
    Enter: Push to Bark (51)
    	A1: Variable Search Replace [ Variable:%astext Search:(http(s)?:\/\/)?[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(\.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+(:[0-9]{1,5})?[-a-zA-Z0-9()@:%_\\\+\.~#?&//=]* Ignore Case:Off Multi-Line:Off One Match Only:On Store Matches In Array:%url Replace Matches:Off Replace With: Continue Task After Error:On ] 
    	A2: If [ %url1 Set ]
    	<修改成自己的Push URL>
    	A3: HTTP Request [  Method:HEAD URL:https://api.day.app/xxxxxxxxxxxx/%e4%bb%8eAndroid%e7%bb%a7%e7%bb%ad?url=%url1 Headers: Query Parameters: Body: File To Send: File/Directory To Save With Output: Timeout (Seconds):10 Trust Any Certificate:Off Automatically Follow Redirects:Off Use Cookies:Off Continue Task After Error:On ] 
    	A4: Else 
    	<修改成自己的Push URL>
    	A5: HTTP Request [  Method:HEAD URL:https://api.day.app/xxxxxxxxxxxx/%astext?automaticallyCopy=1 Headers: Query Parameters: Body: File To Send: File/Directory To Save With Output: Timeout (Seconds):10 Trust Any Certificate:Off Automatically Follow Redirects:Off Use Cookies:Off Continue Task After Error:On ] 
    	A6: End If 
    	A7: If [ %http_response_code ~ 200 ]
    	A8: Flash [ Text:Pushed to Bark Long:Off ] 
    	A9: Else 
    	A10: Flash [ Text:Failed to Push Long:Off ] 
    	A11: End If 
```

---

## 转发验证码

这个Profile会把接收的验证码短信自动转发到Bark，并在iOS端自动复制验证码。如果转发失败则回退到以短信方式转发

> [参与讨论或反馈](https://meta.appinn.net/t/19650)

导入Profile[^4]，或者按下面的描述手动创建Profile

导入完成后记得配置Bark的Push URL和接收转发的手机号码

```
    Profile: 验证码转发
    	Restore: no
    	Event: Received Text [ Type:SMS Sender:* Content:* SIM Card:* ]
    Enter: Anon
    	A1: If [ %SMSRB ~R (验证|校验|安全|authentication|security)(码|code) | %SMSRB ~R (密码|password) ]
    	A2: Variable Search Replace [ Variable:%SMSRB Search:\d{4,8} Ignore Case:Off Multi-Line:Off One Match Only:On Store Matches In Array:%CODE Replace Matches:Off Replace With: ] 
    	<改成你自己的Push URL>
    	A3: HTTP Request [  Method:HEAD URL:https://api.day.app/xxxxxxxxxxxxxxxx/%SMSRB?copy=%CODE1&automaticallycopy=1&isArchive=1 Headers: Query Parameters: Body: File To Send: File/Directory To Save With Output: Timeout (Seconds):10 Trust Any Certificate:Off Automatically Follow Redirects:Off Use Cookies:Off Continue Task After Error:On ] 
    	<回退以短信方式转发>
    	A4: [X] Send SMS [ Number:xxxxxxxxxxx Message:%SMSRB Store In Messaging App:Off SIM Card: Wait For Result:Off ] If [ %http_response_code !~ 200 ]
    	A5: End If 
```

更多转发短信Profiles：

[用短信转发](/offline-sms-forward/) | [用Pushbullet或短信转发](/pushbullet/#短信转发)