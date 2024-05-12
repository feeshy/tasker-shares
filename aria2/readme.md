[^1]: import from [github](https://github.com/feeshy/tasker-shares/raw/master/aria2/aria2.prf.xml) or [taskernet](https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3AAria2)

# Aria2 远程下载

## 完整配置过程

https://feeshy.github.io/tech/aria2

## Tasker配置

需要安装[Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) 和 [AutoShare](https://play.google.com/store/apps/details?id=com.joaomgcd.autoshare)

1.  打开 AutoShare，进入 Share Targets，勾选 AutoShare Command
2.  打开 AutoShare，进入 Manage Commands，新建一个名为 `Aria2` 的 Command，设置一个你喜欢的图标
3.  如果是第一次使用Tasker，先打开Tasker授予必要权限
4.  导入[^1]这个Profile，然后在Tasker任务中手动填写RPC信息
5.  在浏览器中长按想下载的文件，选择AutoShare Commands，然后选择Aria2