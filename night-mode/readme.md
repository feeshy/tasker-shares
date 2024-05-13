[^night]: import from [github](night-mode.prf.xml)
[^day]: import from [github](day-mode.prf.xml)

# Day/Night Mode

Night Mode, Do Not Disturb, System Volume, Auto-Sync, Airplane Mode (root required for airplane mode)

定时切换夜间模式、免打扰模式、系统音量、同步、飞行模式（其中飞行模式需要root权限）

## Description

导入profile[^night]，或者按照以下描述手动创建

```
Profile: Night Mode
	Cooldown: 43200 Restore: no Notification: no
	Time: From 23:00 Till 04:30
Enter: Night Mode
	A1: Night Mode [ Mode:On ] 
	A2: Do Not Disturb [ Mode:Alarms ] 
	A3: System Volume [ Level:0 Display:Off Sound:Off ] 
	A4: Auto-Sync [ Set:Off ] 
	A5: Airplane Mode [ Set:On ] 
```

导入profile[^day]，或者按照以下描述手动创建

```
Profile: Day Mode
	Cooldown: 43200 Restore: no Notification: no
	Time: From 07:30 Till 19:00
Enter: Day Mode
	A1: Night Mode [ Mode:Off ] 
	A2: Do Not Disturb [ Mode:Allow All ] 
	A3: System Volume [ Level:1 Display:Off Sound:Off ] 
	A4: Auto-Sync [ Set:On ] 
	A5: Airplane Mode [ Set:Off ]
```
